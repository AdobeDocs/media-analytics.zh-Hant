---
title: 說明實作媒體 SDK
description: 瞭解如何在行動裝置、OTT和瀏覽器(JS)應用程式中設定Media SDK進行媒體追蹤。
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 94%

---

# 舊版 - Media SDK 設定概觀 {#setup-overview}

當您為視訊應用程式或播放器下載 Media SDK 後，請依照本章節中的資訊設定和實作 Media SDK。


## 一般實作指引 {#general-implementation-guidelines}

使用串流媒體服務進行追蹤時，主要使用三個SDK元件：
* 媒體心率設定 - `MediaHeartbeatConfig` 包含報表的基本設定。
* 媒體心率代理人 - `MediaHeartbeatDelegate` 可控制播放時間和 QoS 物件。
* 媒體心率 - `MediaHeartbeat` 是包含成員與方法的主要程式庫。

## 實作 Streaming Media SDK

若要設定和使用 Streaming Media SDK，請完成以下實作步驟：

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

* **&#x200B; Media Analytics (心率) 伺服器**
此格式一律為「`[your_namespace].hb.omtrdc.net`」。「`[your_namespace]`」會指定您的公司，並且由 Adobe 提供。

媒體追蹤的運作方式在所有平台、桌上型電腦及行動裝置上都一樣。目前音訊追蹤可在行動平台運作。在所有追蹤呼叫中，有一些要驗證的關鍵通用變數：
