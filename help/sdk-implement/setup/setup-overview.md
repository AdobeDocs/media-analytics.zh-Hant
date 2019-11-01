---
title: 設定概觀
description: 在您的行動裝置、OTT和瀏覽器(JS)應用程式中設定媒體追蹤的媒體SDK概觀。
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 設定概觀{#setup-overview}

>[!IMPORTANT]
>
>下列指示適用於2.x Media SDK。 若您正在實施 Media SDK 1.x 版，請參閱 [1.x Media SDK 文件。](/help/sdk-implement/download-sdks.md) 如需Primetime整合商，請參 _閱以下Primetime Media SDK檔案_ 。


## 最低平台版本支援 {#minimum-platform-version}

下表說明自2019年2月19日起，每個SDK支援的最低平台版本。

| 作業系統／瀏覽器 | 需要的最小版本 |
| --- | --- |
| iOS 應用程式 | iOS 6+ |
| Android | Android 5.0+ —— 棒棒糖 |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般實施指引 {#general-implementation-guidelines}

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

1. 實作 `MediaHeartbeatDelegate`.

   |  方法名稱  |  說明  | 必填 |
   | --- | --- | :---: |
   | `getQoSObject()` | 傳回包含目前 QoS 資訊的 `MediaObject` 例項。將在播放工作階段期間呼叫此方法多次。播放器實施必須一律傳回最新可用的 QoS 資料。 | 是 |
   | `getCurrentPlaybackTime()` | 傳回播放點的目前位置。對於 VOD 追蹤，該值是從媒體項目的開頭開始以秒為單位指定的。對於 LINEAR/LIVE 追蹤，該值是從節目的開頭開始以秒為單位指定的。 | 是 |

   >[!TIP]
   >
   >服務質量(QoS)對象是可選的。 若 QoS 資料可供您的播放器使用，且您希望追蹤該資料，則需要下列變數:

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
   >`MediaHeartbeat` 需要執行個 `AppMeasurement` 體來傳送呼叫至Adobe Analytics。

1. 組合所有片段。

   以下範例程式碼將 JavaScript 2.x SDK 用於 HTML5 視訊播放器:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
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

## 驗證 {#validate}

媒體分析追蹤實施會產生兩種類型的追蹤呼叫：

* 媒體和廣告開始呼叫會直接傳送至Adobe Analytics(AppMeasurement)伺服器。
* 心率呼叫會傳送至Media Analytics（心率）追蹤伺服器，並在該處處理，然後傳遞至Adobe Analytics伺服器。

* **Adobe Analytics(AppMeasurement)伺服器如需追蹤伺**&#x200B;服器選項的詳細資訊，請參 [閱正確填入trackingServer和trackingServerSecure變數。](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience cloud訪客ID服務需要解析為RDC伺服器的RDC追蹤伺服器或CNAME。

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Media Analytics(Heartbeats)伺服器**此格式一律為「`[your_namespace].hb.omtrdc.net`」。 「」的值會指`[your_namespace]`定您的公司，並由Adobe提供。

媒體追蹤的運作方式在所有平台、桌上型電腦及行動裝置上都一樣。音訊追蹤目前適用於行動平台。 在所有追蹤呼叫中，有一些要驗證的關鍵通用變數:

## SDK 1.x檔案 {#sdk-1x-documentation}

| 視訊分析1.x SDK |  開發人員指南（僅限PDF） |
| --- | --- |
| Android | [為 Android 進行配置 ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [為 AppleTV 進行配置 ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [為 Chromecast 進行配置 ](chromecast_1.x_sdk.pdf) |
| iOS 應用程式 | [為 iOS 進行配置 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [為 JavaScript 進行配置 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [為 TVML 進行配置 ](vhl_tvml.pdf) |

## Primetime Media SDK 文件 {#primetime-docs}

* [Primetime使用指南](https://helpx.adobe.com/primetime/user-guide.html)
