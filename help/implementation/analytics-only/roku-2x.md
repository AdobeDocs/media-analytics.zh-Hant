---
title: 設定適用於串流媒體的Roku 2.x
description: 安裝並設定適用於Roku的Adobe Media SDK 2.x，以實施僅限Analytics的串流媒體，包括SceneGraph頻道。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# 設定適用於串流媒體的Roku 2.x

Roku適用的Adobe Media SDK 2.x (`adbmobile.brs`)會將來自以BrightScript撰寫的Roku頻道的串流媒體資料直接傳送到Adobe Analytics。 它也會透過Audience Manager收集受眾資料，並透過媒體事件測量參與度。

>[!NOTE]
>
>本頁涵蓋Roku適用的僅限Analytics的Media SDK 2.x。 若是新的實作，Adobe建議[Roku Edge SDK](/help/implementation/edge/roku.md)，此工具可讓Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP以及Adobe Analytics也能使用資料。

* **必要條件**：
   * 完成[僅限Analytics的實作概觀](overview.md)。
   * [下載Roku的Media SDK](/help/getting-started/download-sdks.md)。
   * 在您的媒體播放器中加入API以訂閱播放器事件，以及加入API以提供媒體名稱和播放點位置等播放器資訊。

## 安裝SDK

`AdobeMobileLibrary-2.*-Roku.zip`下載包含兩個元件：

* `adbmobile.brs`：程式庫檔案。 將其複製到通道的`pkg:/source/`目錄中。
* `ADBMobileConfig.json`：針對您的應用程式自訂的SDK設定檔案。

對於SceneGraph頻道，也將`adbmobileTask.brs`和`adbmobileTask.xml`複製到您的`pkg:/components/`目錄中。 請參閱[SceneGraph支援](#scenegraph)。

## 設定ADBMobileConfig.json

組態JSON具有串流媒體的專用`mediaHeartbeat`金鑰。 新增`ADBMobileConfig.json`至您的專案來源並設定`mediaHeartbeat`、`marketingCloud`和`analytics`值：

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| 設定引數 | 說明 |
| --- | --- |
| `server` | 媒體追蹤端點的URL。 檢視僅限[Analytics的實作概觀](overview.md)。 |
| `publisher` | 內容發佈者唯一識別碼。 |
| `channel` | 內容發佈管道的名稱。 回報為[內容管道](/help/implementation/variables/core/content-channel.md)。 |
| `ssl` | SSL是否用於追蹤呼叫。 |
| `ovp` | 線上視訊平台提供者的名稱。 |
| `sdkVersion` | 應用程式或SDK的目前版本。 |
| `playerName` | 播放器名稱。 回報為[內容播放器名稱](/help/implementation/variables/core/content-player-name.md)。 |

>[!IMPORTANT]
>
>如果`mediaHeartbeat`的設定不正確，媒體模組會進入錯誤狀態並停止傳送追蹤呼叫。 確定您的`marketingCloud.org`值包含`@AdobeOrg`。

## 初始化SDK並處理訊息

取得具有`ADBMobile()`的SDK執行個體。 Experience Cloud訪客ID服務會產生一個包含在所有點選中的訪客ID。

>[!IMPORTANT]
>
>每隔250毫秒呼叫主事件回圈中的`processMessages`和`processMediaMessages`，讓SDK正確傳送ping。

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| 方法 | 說明 |
| --- | --- |
| `processMessages` | 將佇列的Analytics事件傳遞至SDK。 |
| `processMediaMessages` | 將佇列的媒體事件傳遞至SDK，包括自動Ping。 |

## 追蹤媒體事件

呼叫其SDK方法以追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Roku 2.x**&#x200B;標籤，以取得確切的呼叫、建置器及常數。

一般工作階段從建立媒體物件並呼叫`mediaTrackSessionStart`開始：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

全域`adb_media_init_*`建置器會建立追蹤呼叫使用的媒體、廣告、廣告插播、章節和QoS物件：

| 產生器 | 簽章 |
| --- | --- |
| 媒體 | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| 廣告 | `adb_media_init_adinfo(name, id, position, length)` |
| 廣告插播 | `adb_media_init_adbreakinfo(name, startTime, position)` |
| 章節 | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

標準中繼資料是以`a.media.*`索引鍵的關聯陣列傳遞（SDK也定義這些索引鍵的具名常數，例如`MEDIA_VideoMetadataKeySHOW`）。 檢視對應至每個維度的索引鍵的[變數](/help/implementation/variables/overview.md)頁面。

## 設定Experience Cloud訪客ID、隱私權和記錄

`ADBMobile()`執行個體上的下列方法可管理身分、隱私權和偵錯：

| 方法 | 說明 |
| --- | --- |
| `visitorMarketingCloudID()` | 擷取Experience Cloud ID (ECID)。 |
| `visitorSyncIdentifiers(identifiers)` | 為相同訪客設定其他客戶ID。 |
| `setAdvertisingIdentifier(rida)` | 設定Advertising的Roku ID (RIDA)。 使用Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API取得。 |
| `getAllIdentifiers()` | 傳回SDK儲存的所有識別碼，包括Analytics、訪客、Audience Manager和自訂識別碼。 |
| `setPrivacyStatus(status)` | 設定隱私權狀態。 傳遞`adb.PRIVACY_STATUS_OPT_IN`或`adb.PRIVACY_STATUS_OPT_OUT`。 請參閱[隱私權](/help/implementation/opt-out-privacy.md)。 |
| `getPrivacyStatus()` | 傳回目前的隱私權狀態。 |
| `setDebugLogging(flag)` | 啟用或停用偵錯記錄。 |
| `getDebugLogging()` | 如果啟用偵錯記錄，則傳回`true`。 |

## SceneGraph支援 {#scenegraph}

Roku SceneGraph XML架構無法直接呼叫舊版BrightScript SDK API，因為SDK使用的元件（例如執行緒）不適用於SceneGraph應用程式。 為了彌補此差距，SDK提供可傳回SceneGraph相容例項的聯結器，公開相同API，並為傳回資料的API提供回呼機制。

橋有三個部分：

* **`adbmobileTask`節點**：在背景執行緒上執行SDK API並將資料傳回場景的SceneGraph工作節點。
* **聯結器執行個體**：封裝所有舊版公用API，並與`adbmobileTask`節點通訊。
* **`API_RESPONSE`回呼**：您的應用程式所觀察的欄位，用於接收來自getter API的傳回值。

若要在SceneGraph頻道中初始化SDK：

1. 將`adbmobile.brs`匯入您的場景：

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. 建立`adbmobileTask`節點、取得聯結器執行個體並載入SceneGraph常數：

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. 註冊回撥以接收傳回資料之API的回應物件：

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

聯結器執行個體(`m.adbmobile`)公開與舊版SDK （`mediaTrackSessionStart`、`mediaTrackPlay`、`mediaTrackPause`、`mediaTrackComplete`、`mediaTrackSessionEnd`、`mediaTrackError`、`mediaTrackEvent`、`mediaUpdatePlayhead`和`mediaUpdateQoS`）相同的媒體方法，因此事件和變數頁面上顯示的呼叫運作方式相同。 直接呼叫Setter API； getter API透過`API_RESPONSE`回呼傳回其值。

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
