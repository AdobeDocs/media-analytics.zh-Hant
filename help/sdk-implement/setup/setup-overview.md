---
seo-title: 設定概述
title: 設定概述
uuid: 06feeddb-b0 c8-4f7 d-90c8-e374 cdd1695
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>下列指示適用於2.x Media SDK。若您正在實施 Media SDK 1.x 版，請參閱 [1.x Media SDK 文件。](/help/sdk-implement/download-sdks.md) 如需Primetime整合商，請參閱 _下面的Primetime媒體SDK文件_ 。


## Minimum Platform Version Support {#minimum-platform-version}

下表說明每個SDK支援的最低平台版本，自2019年月19日起。

| OS/瀏覽器 | 需要最低版本 |
| --- | --- |
| iOS 應用程式 | iOS 6+ |
| Android | Android5.0+- Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v+ |
| IE | v11+ |

## 一般實施指引 {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

有三個主要的 SDK 元件與媒體追蹤有關:
* 媒體心率設定 - 此設定包含報表的基本設定。
* 媒體心率代理人 - 代理人可控制播放時間和 QoS 物件。
* 媒體心率 - 包含成員與方法的主要程式庫。

完成下列實作步驟：

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  變數名稱  | 說明  | 必填 |  預設值  |
   |---|---|:---:|---|
   | `trackingServer` | 適用於媒體分析的追蹤伺服器。這與您的分析追蹤伺服器不同。 | 是 | 空白字串 |
   | `channel` | 管道名稱 | 無 | 空白字串 |
   | `ovp` | 線上媒體平台的名稱，透過它分送內容 | 無 | 空白字串 |
   | `appVersion` | 媒體播放器應用程式/SDK 的版本 | 無 | 空白字串 |
   | `playerName` | 使用的媒體播放器名稱，例如「AVPlayer」、「HTML5 播放器」、「我的自訂播放器」 | 無 | 空白字串 |
   | `ssl` | 指出呼叫是否應透過 HTTPS 進行 | 無 | false |
   | `debugLogging` | 指出是否已啟用除錯記錄 | 無 | false |

1. Implement the `MediaHeartbeatDelegate`.

   |  方法名稱  |  說明  | 必填 |
   | --- | --- | :---: |
   | `getQoSObject()` | 傳回包含目前 QoS 資訊的 `MediaObject` 例項。將在播放工作階段期間呼叫此方法多次。播放器實施必須一律傳回最新可用的 QoS 資料。 | 是 |
   | `getCurrentPlaybackTime()` | 傳回播放點的目前位置。對於 VOD 追蹤，該值是從媒體項目的開頭開始以秒為單位指定的。對於 LINEAR/LIVE 追蹤，該值是從節目的開頭開始以秒為單位指定的。 | 是 |

   >[!TIP]
   >
   >服務品質(QoS)物件為選用項目。若 QoS 資料可供您的播放器使用，且您希望追蹤該資料，則需要下列變數:

   | 變數名稱 | 說明   | 必填 |
   | --- | --- | :---: |
   | `bitrate` | 媒體的位元速率，以每秒位元組數為單位。 | 是 |
   | `startupTime` | 媒體的啟動時間 (以毫秒為單位) | 是 |
   | `fps` | 每秒顯示的畫面。 | 是 |
   | `droppedFrames` | 目前掉格的數量。 | 是 |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. 此例項將用於下列所有媒體追蹤事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要傳送呼叫給Adobe `AppMeasurement` Analytics的例項。

1. 組合所有片段。

   以下範例程式碼將 JavaScript 2.x SDK 用於 HTML5 視訊播放器:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## 驗證 {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

媒體實作包含兩種類型的追蹤呼叫:

* 媒體和廣告開始呼叫會直接傳送到 AppMeasurement 伺服器。
* 心率呼叫會在開始時傳送至心率追蹤伺服器，內容每十秒傳送一次，廣告每一秒傳送一次。

媒體追蹤的運作方式在所有平台、桌上型電腦及行動裝置上都一樣。目前，音效追蹤可在行動平台運作。在所有追蹤呼叫中，有一些要驗證的關鍵通用變數:

* **AppMeasurement(Analytics)**&#x200B;如需追蹤伺服器選項的詳細資訊，請參閱 [正確填入trackingServer和trackingServerSecure變數。](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience Cloud訪客ID服務需要RDC追蹤伺服器或CNAME解析至RDC伺服器。

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* **活動訊號(Media Analytics)**&#x200B;一律有格式「`[namespace].hb.omtrdc.net`，其中」`[namespace]`是由您的登入公司定義，由Adobe提供。

## SDK 1.x Documentation {#section_acj_tkk_t2b}

| Video Analytics1.x SDK | 開發人員指南(僅限PDF) |
| --- | --- |
| Android | [為 Android 進行配置 ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [為 AppleTV 進行配置 ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [為 Chromecast 進行配置 ](chromecast_1.x_sdk.pdf) |
| iOS 應用程式 | [為 iOS 進行配置 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [為 JavaScript 進行配置 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [為 TVML 進行配置 ](vhl_tvml.pdf) |

## Primetime Media SDK 文件 {#primetime-docs}

* [Primetime使用者指引](https://helpx.adobe.com/primetime/user-guide.html)
