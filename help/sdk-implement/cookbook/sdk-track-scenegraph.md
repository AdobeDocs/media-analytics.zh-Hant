---
title: 在 SceneGraph (Roku) 中進行追蹤
description: 了解如何使用Roku SceneGraph XML程式設計架構追蹤媒體。
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 98%

---

# 在 SceneGraph (Roku) 中進行追蹤{#tracking-in-scenegraph-roku}

## 簡介 {#introduction}

Roku 已推出開發應用程式的新程式設計架構：SceneGraph XML 程式設計架構。此新架構有兩個新的重要概念：

* SceneGraph 演算應用程式畫面
* SceneGraph 畫面的 XML 設定

Adobe Mobile SDK for Roku 是以 BrightScript 編寫。此 SDK 有許多元件不適用於 SceneGraph 上執行的應用程式 (如執行緒)。因此，想使用 SceneGraph 架構的 Roku 應用程式開發人員，無法呼叫 Adobe Mobile SDK API (後者類似於舊版 BrightScript 應用程式中的 API)。

## 架構 {#architecture}

為了將 SceneGraph 支援加入 AdobeMobile SDK，Adobe 已新增一個新的 API，該 API 在 AdobeMobile SDK 和 `adbmobileTask` 之間建立連接器橋接器。後者是用於 SDK 之 API 執行的 SceneGraph 節點。(在本文件其他章節中詳細說明 `adbmobileTask` 的用法。)

連接器橋接器專為執行下列功能所設計：

* 橋接器會傳回 Adobe Mobile SDK 與 SceneGraph 相容的執行個體。與 SceneGraph 相容的 SDK 包含舊版 SDK 揭露的所有 API。
* 您在 SceneGraph 中使用 Adobe Mobile SDK API 的方式，與使用舊版 API 的方式非常類似。
* 橋接器也會揭露機制，監聽傳回部分資料的 API 回呼。

![](assets/SceneGraph_arch.png)

## 元件 {#components}

**SceneGraph 應用程式：**

* 透過 SceneGraph 連接器橋接器 API 使用 `AdobeMobileLibrary` API。
* 針對預期的輸出資料變數在 `adbmobileTask` 上註冊回應回呼。

**AdobeMobileLibrary：**

* 揭露一組公用 API (舊版)，包括連接器橋接器 API。
* 傳回納入所有舊版公用 API 的 SceneGraph 連接器執行個體。
* 與 `adbmobileTask` SceneGraph 節點通訊以執行 API。

**adbmobileTask 節點：**

* 在背景執行緒上執行 `AdobeMobileLibrary` API 的 SceneGraph 任務節點。
* 作為委派以將資料傳回應用程式場景。

## 公用 SceneGraph API {#public-scenegraph-apis}

### ADBMobileConnector

| 類別 | 方法名稱 | 說明 |
|---|---|---|
| **常數** |  |  |
|  | `sceneGraphConstants` | 傳回包含 `SceneGraphConstants` 的物件。如需詳細資料，請參閱上表。 |
|  |  |  |
| **除錯記錄** |  |  |
|  | `setDebugLogging` | SceneGraph API 可在 ADBMobile SDK 上設定除錯記錄。 |
|  | `getDebugLogging` | SceneGraph API 可在 ADBMobile SDK 上取得除錯記錄。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「除錯記錄」區段。 |  |
|  |  |  |
| **隱私權狀態 / 選擇退出** |  |  |
|  | `setPrivacyStatus` | SceneGraph API 可在 ADBMobile SDK 上設定隱私權狀態。 |
|  | `getPrivacyStatus` | SceneGraph API 可在 ADBMobile SDK 上取得隱私權狀態。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「選擇退出/隱私權狀態」區段。 |  |
|  |  |  |
| **Analytics** |  |  |
|  | `trackState` | SceneGraph API 可在 ADBMobile SDK 上追蹤狀態。 |
|  | `trackAction` | SceneGraph API 可在 ADBMobile SDK 上追蹤動作。 |
|  | `trackingIdentifier` | SceneGraph API 可從 ADBMobile SDK 上取得追蹤識別碼。 |
|  | `userIdentifier` | SceneGraph API 可從 ADBMobile SDK 上取得使用者識別碼。 |
|  | `setUserIdentifier` | SceneGraph API 可從 ADBMobile SDK 上設定使用者識別碼。 |
|  | `getAllIdentifiers` | SceneGraph API 會擷取已知且由 Roku SDK 保存的所有使用者身分識別資料。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「Analytics」區段。 |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | SceneGraph API 可從 ADBMobile SDK 上同步 Experience Cloud 識別碼。 |
|  | `visitorMarketingCloudID` | SceneGraph API 可從 ADBMobile SDK 上取得 Experience Cloud ID。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「Experience Cloud」一節。 |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | SceneGraph API 使用特徵傳送對象管理訊號。 |
|  | `audienceVisitorProfile` | SceneGraph API 可從 ADBMobile SDK 取得 Audience Manager 訪客設定檔。 |
|  | `audienceDpid` | SceneGraph API 可從 ADBMobile SDK 取得對象 Dpid。 |
|  | `audienceDpuuid` | SceneGraph API 可從 ADBMobile SDK 取得對象 Dpuuid。 |
|  | `audienceSetDpidAndDpuuid` | SceneGraph API 可在 ADBMobile SDK 上設定對象 Dpid 和 Dpuuid。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「Audience Manager」一節。 |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | 載入影片內容以追蹤 MediaHeartbeat 的 SceneGraph API。 |
|  | mediaTrackStart | 使用 MediaHeartbeat 開始影片追蹤工作階段的 SceneGraph API。 |
|  | `mediaTrackUnload` | SceneGraph API 可從 MediaHeartbeat 追蹤卸載影片內容。 |
|  | `mediaTrackPlay` | 追蹤播放影片內容的 SceneGraph API。 |
|  | mediaTrackPause | 追蹤暫停影片內容的 SceneGraph API。 |
|  | `mediaTrackComplete` | 追蹤影片內容播放完成的 SceneGraph API。 |
|  | `mediaTrackError` | 追蹤播放錯誤的 SceneGraph API。 |
|  | mediaTrackEvent | 在追蹤期間追蹤播放事件的 SceneGraph API。例如「廣告」、「章節」。 |
|  | `mediaUpdatePlayhead` | SceneGraph API 可在影片追蹤期間將播放點更新傳送至 MediaHeartbeat。 |
|  | `mediaUpdateQoS` | SceneGraph API 可在影片追蹤期間將 QoS 更新傳送至 MediaHeartbeat。 |
|  | 如需更多資訊，請參閱舊版 SDK 的「MediaHeartbeat」一節。 |  |

### SceneGraphConstants

| 常數名稱 | 說明 |
|---|---|
| `API_RESPONSE` | 用於從 `adbmobileTask` 節點的 `adbmobileApiResponse` 欄位擷取回應物件 |
| `DEBUG_LOGGING` | 做為適用於 `getDebugLogging` 的 `apiName` |
| `PRIVACY_STATUS` | 做為適用於 `getPrivacyStatus` 的 `apiName` |
| `TRACKING_IDENTIFIER` | 做為適用於 `trackingIdentifier` 的 `apiName` |
| `USER_IDENTIFIER` | 做為適用於 `userIdentifier` 的 `apiName` |
| `VISITOR_MARKETING_CLOUD_ID` | 做為適用於 `visitorMarketingCloudID` 的 `apiName` |
| `AUDIENCE_VISITOR_PROFILE` | 做為適用於 `audienceVisitorProfile` 的 `apiName` |
| `AUDIENCE_DPID` | 做為適用於 `audienceDpid` 的 `apiName` |
| `AUDIENCE_DPUUID` | 做為適用於 `audienceDpuuid` 的 `apiName` |

### adbmobileTask 節點

<table>
<thead>
<tr>
<td> 欄位 </td><td> 類型 </td><td> 預設 </td><td> 使用狀況 </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Invalid </td>
<td> 請勿修改此欄位或讓應用程式使用此欄位。此欄位由 ADBMobile SceneGraphConnector 用於透過 SceneGraph 節點路由 API 呼叫並擷取回應。因此，此索引鍵/欄位已針對 SceneGraph 相容性保留供 AdobeMobileSDK 使用。<b>重要：</b>此欄位的任何修改都可能導致 AdobeMobileSDK 無法正常運作。</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> 無效 </td>
<td> 唯讀：在 AdobeMobileSDK 上執行的所有 API 將在此欄位上傳回回應。登錄回呼以監聽此欄位的更新，以接收回應物件。回應物件的格式如下：  
<pre>
response = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt; 
  "returnValue : &lt;API_RESPONSE&gt; 
}</pre>
此回應物件的例項將在 AdobeMobileSDK 上針對任何 API 呼叫傳送，預計該 API 呼叫會根據 API 參考指南傳回值。例如，visitorMarketingCloudID() 的 API 呼叫將傳回以下回應物件： 
<pre>
response = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
} 
</pre>
或者，回應資料也可能無效： 
<pre>
response = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : invalid 
} 
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API 簽章：`ADBMobile().getADBMobileConnectorInstance()`\
輸入：`adbmobileTask`
傳回類型：`ADBMobileConnector`

#### `sgConstants`

API 簽章：`ADBMobile().sgConstants()`
輸入：無\
傳回類型：`SceneGraphConstants`

>[!NOTE]
>如需詳細資料，請參閱 `ADBMobileConnector` API 參考資料。

### ADBMobile 常數

|  功能  | 常數名稱 | 說明 |
|---|---|---|
| 版本設定 | `version` | 用於擷取 AdobeMobileLibrary 版本資訊的常數 |
| 隱私權/選擇退出 | `PRIVACY_STATUS_OPT_IN` | 隱私權狀態選擇加入的常數 |
|  | `PRIVACY_STATUS_OPT_OUT` | 隱私權狀態選擇退出的常數 |
| MediaHeartbeat 常數 | 請參閱此頁面的常數：<br/><br/>[媒體心率方法](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md)。 | 將這些常數與 MediaHeartbeat API 搭配使用 |
| 標準中繼資料 | 請參閱此頁面的常數：<br/><br/>[標準中繼資料參數](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)。 | 使用這些常數附加 MediaHeartbeat API 中的標準影片/廣告中繼資料 |

傳統 AdobeMobileLibrary 上全域定義之公用程式 `MediaHeartbeat` API 的存取方式&#x200B;*如同*&#x200B;在 SceneGraph 環境中存取一樣，因為這些 API 未使用任何在 SceneGraph 節點中無法使用的 Brightscript 元件。如需這些方法的詳細資訊，請參閱下表：

### 適用於 MediaHeartbeat 的全域方法

| 方法 | 說明 |
| --- | --- |
| `adb_media_init_mediainfo` | 此方法會傳回初始化的媒體資訊物件 `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | 此方法會傳回初始化的廣告資訊物件 `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | 此方法會傳回初始化的章節資訊物件。`Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | 此方法會傳回初始化的 AdBreak 資訊物件。`Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | 此方法會傳回初始化的 QoS 資訊物件。`Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## 實作 {#implementation}

1. **下載 Roku 程式庫 -** 下載[最新 Roku 程式庫](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)。

1. **設定您的開發環境**

   1. 將 `adbmobile.brs` (AdobeMobileLibrary) 複製至您的 `pkg:/source/` 目錄。

   1. 如需「場景圖形」支援，請將 `adbmobileTask.brs` 和 `adbMobileTask.xml` 複製至您的 `pkg:/components/` 目錄。

1. **初始化**

   1. 將 `adbmobile.brs` 匯入您的「場景」。

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. 將 `adbmobileTask` 節點例項建立在您的場景中。

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. 使用 `adbmobile` 例項取得 SceneGraph 適用的instance of `adbmobileTask` 連接器例項。 

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. 取得 `adbmobile` SG 常數。

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. 註冊回撥以便為所有 `AdbMobile` API 呼叫接收回應物件。

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse") 
      
      ' Sample implementation of the callback 
      ' Listen for all the constants for which API calls are made on the SDK 
      function onAdbmobileApiResponse() as void 
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
      
          if responseObject <> invalid 
              methodName = responseObject.apiName 
              retVal = responseObject.returnValue 
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING 
                  if retVal 
                      print "API Response: DEBUG LOGGING: " + "True" 
                  else 
                      print "API Response: DEBUG LOGGING: " + "False" 
                  endif 
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS 
                  print "API Response: PRIVACY STATUS: " + retVal 
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: TRACKING IDENTIFIER: " + retVal 
                  else 
                      print "API Response: TRACKING IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: USER IDENTIFIER: " + retVal 
                  else 
                      print "API Response: USER IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID 
                  if retVal <> invalid 
                      print "API Response: MCID: " + retVal 
                  else 
                      print "API Response: MCID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPUUID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPUUID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object" 
                  else 
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid" 
                  endif 
              endif 
          endif 
      end function 
      ```

## 實作範例 {#sample-implementation}

### 舊版 SDK 上的 API 呼叫範例

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### SG SDK 上的 API 呼叫範例

```
'create adbmobileTask instance 
m.adbmobileTask = createObject("roSGNode", "adbmobileTask") 
   
'get an instance of SDK using task instance 
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask) 
m.adbmobileConstants = m.adbmobile.sceneGraphConstants() 
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
  
'execute getter APIs 
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse") 
m.adbmobile.getDebugLogging() 
   
'listen for return data in registered callbacks 
function onAdbmobileApiResponse() as void 
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
  
        if responseObject <> invalid 
            methodName = responseObject.apiName 
            retVal = responseObject.returnValue 
  
        if methodName = m.adbmobileConstants.DEBUG_LOGGING 
            if retVal 
                print "API Response: DEBUG LOGGING: " + "True" 
            else 
                print "API Response: DEBUG LOGGING: " + "False" 
         endif 
    endif 
end function
```
