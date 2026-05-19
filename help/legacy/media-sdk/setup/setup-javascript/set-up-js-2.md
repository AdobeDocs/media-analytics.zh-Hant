---
title: 如何使用 JavaScript 2.x 設定 Media SDK
description: 請依照這些步驟在 JavaScript 2.x 上設定 Media SDK 應用程式。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mYfKt95xUE59MuMFOzGro6fPsJsdy4wcy2F2J--JaW8
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 89%

---

# 設定 JavaScript 2.x{#set-up-javascript}

## 先決條件

* **取得有效的設定引數**
設定Analytics帳戶後，可以向Adobe代表取得這些引數。
* 在您的媒體應用程式中&#x200B;**實作JavaScript的`AppMeasurement`**
如需Adobe Mobile SDK檔案的詳細資訊，請參閱[使用JavaScript實作Analytics。](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant)

* **在您的媒體播放器中提供下列功能：**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等詳細內容。

1. 將[下載的](/help/getting-started/download-sdks.md)程式庫新增至專案。 為方便起見，請建立類別的本機參照。

   1. 展開您下載的 `MediaSDK-js-v2.*.zip` 檔案。
   1. 驗證 `MediaSDK.min.js` 目錄中存在 `libs` 檔案：

   1. 主控 `MediaSDK.min.js` 檔案。

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。 下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.min.js`

      在每一頁的 `<head>` 或 `<body>` 標籤中新增下列程式碼行，加入 JavaScript 適用的 `MediaSDK`。 例如：

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

   以下示範 `MediaHeartbeatConfig` 初始化：

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

1. 實作 `MediaHeartbeatDelegate` 通訊協定。

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
   >請確保您的 `MediaHeartbeat` 例項可供存取，並且不會在媒體工作階段結束前遭到取消配置。 此例項將用於下列所有追蹤事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的例項，才能傳送呼叫至 Adobe Analytics。 以下是 `AppMeasurement` 例項的範例：

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## 從 JavaScript 1.x 移轉至 2.x

在 2.x 版中，所有公用方法皆已整合至 `ADB.va.MediaHeartbeat` 類別，讓開發人員更容易操作。 此外，所有的設定現已整合至 `ADB.va.MediaHeartbeatConfig` 類別。

如需有關從 1.x 移轉至 2.x 的資訊，請參閱舊版實作文件。
