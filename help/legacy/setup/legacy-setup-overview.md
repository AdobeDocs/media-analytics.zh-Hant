---
title: 說明實作舊版 Media SDK
description: 了解如何在行動裝置、OTT 和瀏覽器 (JS) 應用程式中設定 **舊版** 2.x Media SDK 進行媒體追蹤。
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 99%

---

# 舊版 2.x Streaming Media SDK 設定概觀{#setup-overview}

本章節中的指示適用於&#x200B;**舊版** 2.x Media SDK。

* 如需有關實作 Media SDK 1.x 版的資訊，請參閱 [1.x Media SDK 文件](/help/getting-started/download-sdks.md)。

* 如需 Primetime 整合器的相關資訊，請參閱 _Primetime Media SDK 文件_。

>[!IMPORTANT]
>
>我們於 2021 年 8 月 31 日停止支援第 4 版 Mobile SDK 後，Adobe 也將停止支援 Media Analytics SDK iOS 版和 Android 版。如需詳細資訊，請參閱 [Media Analytics SDK 支援終止常見問題集](/help/additional-resources/end-of-support-faqs.md)。


## 最低平台版本支援 {#minimum-platform-version}

下表說明自 2019 年 2 月 19 日起各個 SDK 支援的最低平台版本。

| 作業系統/瀏覽器 | 需要的最低版本 |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般實作指引 {#general-implementation-guidelines}

有三個主要的 SDK 元件與媒體追蹤有關：
* 媒體心率設定 - 此設定包含報表的基本設定。
* 媒體心率代理人 - 代理人可控制播放時間和 QoS 物件。
* 媒體心率 - 包含成員與方法的主要程式庫。

完成下列實作步驟：

1. 建立 `MediaHeartbeatConfig` 例項並設定您的設定參數值。

   |  變數名稱 | 說明 | 必填 |  預設值  |
   |---|---|:---:|---|
   | `trackingServer` | 適用於媒體分析的追蹤伺服器。這與您的分析追蹤伺服器不同。 | 是 | 空字串 |
   | `channel` | 頻道名稱 | 無 | 空字串 |
   | `ovp` | 線上媒體平台的名稱，透過它分送內容 | 無 | 空字串 |
   | `appVersion` | 媒體播放器應用程式/SDK 的版本 | 無 | 空字串 |
   | `playerName` | 使用的媒體播放器名稱，例如「AVPlayer」、「HTML5 播放器」、「我的自訂播放器」 | 無 | 空字串 |
   | `ssl` | 指出是否應透過 HTTPS 進行呼叫 | 無 | false |
   | `debugLogging` | 指出是否已啟用除錯記錄 | 無 | false |

1. 實作 `MediaHeartbeatDelegate`。

   |  方法名稱  |  說明 | 必填 |
   | --- | --- | :---: |
   | `getQoSObject()` | 傳回包含目前 QoS 資訊的 `MediaObject` 例項。將在播放工作階段期間呼叫此方法多次。播放器實作必須一律傳回最新可用的 QoS 資料。 | 是 |
   | `getCurrentPlaybackTime()` | 傳回播放點的目前位置。<br /> 對於 VOD 追蹤，此值是從媒體項目的開頭開始以秒為單位指定的。<br /> 對於直播串流，如果播放器未提供內容持續時間的相關資訊，則此值可以指定為自當天 UTC 午夜開始的秒數。<br /> 注意：使用進度標記時，需要內容持續時間，並且播放點需要更新為從媒體項目開始的秒數，從 0 開始。 | 是 |

   >[!TIP]
   >
   >服務品質 (QoS) 物件為選用。若 QoS 資料可供您的播放器使用，且您希望追蹤該資料，則需要下列變數：

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `bitrate` | 媒體的位元速率 (以每秒位元組數為單位)。 | 是 |
   | `startupTime` | 媒體的啟動時間 (以毫秒為單位) | 是 |
   | `fps` | 每秒顯示的畫面。 | 是 |
   | `droppedFrames` | 目前掉格的數量。 | 是 |

1. 建立 `MediaHeartbeat` 例項。

   使用 `MediaHertbeatConfig` 和 `MediaHertbeatDelegate` 來建立 `MediaHeartbeat` 例項。

   >[!IMPORTANT]
   >
   >請確保您的 `MediaHeartbeat` 例項可供存取，並且不會在工作階段結束前遭到取消配置。此例項將用於下列所有媒體追蹤事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的例項，才能傳送呼叫至 Adobe Analytics。

1. 組合所有片段。

   以下範例程式碼將 JavaScript 2.x SDK 用於 HTML5 視訊播放器：

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

Media Analytics 追蹤實作會產生兩種類型的追蹤呼叫：

* 媒體和廣告開始呼叫會直接傳送到 Adobe Analytics (AppMeasurement) 伺服器。
* 心率呼叫會傳送到 Media Analytics (心率) 追蹤伺服器並於該位置處理，然後再傳遞到 Adobe Analytics 伺服器。

* **Adobe Analytics (AppMeasurement) 伺服器**
如需有關追蹤伺服器選項的詳細資訊，請參閱[正確填入 trackingServer 和 trackingServerSecure 變數](https://helpx.adobe.com/tw/analytics/kb/determining-data-center.html)。

  >[!IMPORTANT]
  >
  >Experience Cloud 訪客 ID 服務需要 RDC 追蹤伺服器，或 CNAME 解析至 RDC 伺服器。

  分析追蹤伺服器的結尾應該是「`.sc.omtrdc.net`」或應該是 CNAME。

* ** Media Analytics (心率) 伺服器**
此格式一律為「`[your_namespace].hb.omtrdc.net`」。「`[your_namespace]`」會指定您的公司，並且由 Adobe 提供。

媒體追蹤的運作方式在所有平台、桌上型電腦及行動裝置上都一樣。目前音訊追蹤可在行動平台運作。在所有追蹤呼叫中，有一些要驗證的關鍵通用變數：

## SDK 1.x 文件 {#sdk-1x-documentation}

| Video Analytics 1.x SDK |  開發人員指南 (僅提供 PDF) |
| --- | --- |
| Android | [為 Android 進行配置](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [設定Apple TV](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [為 Chromecast 進行配置](chromecast_1.x_sdk.pdf) |
| iOS | [為 iOS 進行配置](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [為 JavaScript 進行配置](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android：[設定 Media Analytics](https://help.adobe.com/zh_TW/primetime/psdk/android/1.4/index.html) </li> <li> DHLS：[設定 Media Analytics](https://help.adobe.com/zh_TW/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS：[設定 Media Analytics](https://help.adobe.com/zh_TW/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [為 TVML 進行配置](vhl_tvml.pdf) |

## Primetime Media SDK 文件 {#primetime-docs}

* [Primetime 使用手冊](https://helpx.adobe.com/tw/primetime/user-guide.html)
