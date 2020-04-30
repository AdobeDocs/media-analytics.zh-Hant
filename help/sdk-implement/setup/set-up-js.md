---
title: 設定 JavaScript
description: 適用於 JavaScript 實施的 Media SDK 應用程式設定。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# 設定 JavaScript{#set-up-javascript}

## 必備條件

* **取得有效的設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的媒體應用程式實作 JavaScript 適用的`AppMeasurement`**
如需有關 Adobe Mobile SDK 文件的詳細資訊，請參閱[利用 JavaScript 實作分析](https://docs.adobe.com/content/help/zh-Hant/analytics/implementation/js/overview.html)。

* **在您的媒體播放器中提供下列功能:**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-2x-sdks)程式庫新增至專案。為方便起見，請建立類別的本機參照。

   1. 展開您下載的 `MediaSDK-js-v2.*.zip` 檔案。
   1. 驗證 `MediaSDK.min.js` 目錄中存在 `libs` 檔案:

   1. 主控 `MediaSDK.min.js` 檔案。

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.min.js`

      在每一頁的 `<head>` 或 `<body>` 標籤中新增下列程式碼行，加入 JavaScript 適用的 `MediaSDK`。例如:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. 若要快速確認程式庫是否已成功匯入，請實例化 `ADB.va.MediaHeartbeatConfig` 類別。

      >[!NOTE]
      >
      >從 2.1.0 版本開始，JavaScript SDK 符合 AMD 和 CommonJS 模組規格，`VideoHeartbeat.min.js` 也可以與相容的模組載入器搭配使用。

1. 請建立對 `MediaHeartbeat` 類別的本機參照，以方便您存取 API。

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. 建立 `MediaHeartbeatConfig` 例項。

   本節可協助您瞭解 `MediaHeartbeat` 設定參數，以及如何在您的 `MediaHeartbeat` 例項上設定正確的設定值，以提高追蹤準確率。

   以下示範 `MediaHeartbeatConfig` 初始化:

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. 實施 `MediaHeartbeatDelegate` 通訊協定。

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. 建立 `MediaHeartbeat` 例項。

   使用 `MediaHeartbeatConfig` 和 `MediaHeartbeatDelegate` 來建立 `MediaHeartbeat` 例項。

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >請確保您的 `MediaHeartbeat` 例項可供存取，並且不會在媒體工作階段結束前遭到取消配置。此例項將用於下列所有追蹤事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的例項，才能傳送呼叫至 Adobe Analytics。以下是 `AppMeasurement` 例項的範例:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## 在 JavaScript 中從 1.x 版移轉至 2.x 版

在 2.x 版中，所有公用方法皆已整合至 `ADB.va.MediaHeartbeat` 類別，讓開發人員更容易操作。此外，所有的設定現已整合至 `ADB.va.MediaHeartbeatConfig` 類別。

如需有關從 1.x 移轉至 2.x 的詳細資訊，請參閱[從 VHL 1.x 移轉至 2.x](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)。
