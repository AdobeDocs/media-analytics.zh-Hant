---
seo-title: 設定 JavaScript
title: 設定 JavaScript
uuid: 0269d8ad-0af8-4df1-9d15-e06 c2952 a005
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# 設定 JavaScript{#set-up-javascript}

## 必備條件

* **取得有效的設定參數**：您可以在設定分析帳戶後，向Adobe代表取得這些參數。
* **在`AppMeasurement`您的媒體應用程式中實施JavaScript**如需有關Adobe
Mobile SDK文件的詳細資訊，請參閱「 [使用JavaScript實施Analytics」。](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **在您的媒體播放器中提供下列功能:**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

1. 將[下載的](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)程式庫新增至專案。為方便起見，請建立類別的本機參照。

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.min.js`

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. 例如:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. 若要快速確認   程式庫是否已成功匯入，請實例化 `ADB.va.MediaHeartbeatConfig` 類別。

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. 請建立對 `MediaHeartbeat` 類別的本機參照，以方便您存取 API。

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

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

1. Implement the `MediaHeartbeatDelegate` protocol.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. 此例項將用於下列所有追蹤事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要傳送呼叫給Adobe `AppMeasurement` Analytics的例項。以下是 `AppMeasurement` 例項的範例:

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

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
