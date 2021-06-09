---
title: 設定 JavaScript 3.x
description: 適用於 JavaScript 3.x 實作的 Media SDK 應用程式設定。
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 100%

---

# 設定 JavaScript 3.x{#set-up-javascript}

## 必備條件

* **取得有效的設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的媒體應用程式實作 JavaScript 適用的 `AppMeasurement` 和 `Experience Cloud Identity Service`**
如需詳細資訊，請參閱[使用 JavaScript 實作分析](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)和[實作 Experience Cloud Identity Service。](https://docs.adobe.com/content/help/zh-Hant/id-service/using/implementation/setup-analytics.html)

* **在您的媒體播放器中提供下列功能：**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 這包含目前播放的媒體、廣告、章節之相關資訊。

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-3x-sdks)程式庫新增至專案。為方便起見，請建立類別的本機參照。

   1. 展開您下載的 `MediaSDK-js-v3*.zip` 檔案。
   1. 驗證 `libs` 目錄中存在 `MediaSDK.js` 檔案。

   1. 主控 `MediaSDK.js` 檔案。

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.js`

      在每一頁的 `<head>` 或 `<body>` 標籤中新增下列程式碼行，加入 JavaScript 適用的 `MediaSDK`。例如：

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. 若要快速確認程式庫是否已成功匯入，請確認 `ADB.Media` 是否已匯出至視窗物件。

      >[!NOTE]
      >
      >JavaScript SDK 符合 AMD 和 CommonJS 模組規格，`MediaSDK.js` 也可以與相容的模組載入器搭配使用。

1. 建立 `AppMeasurement` 的例項和設定 `visitor`。

   Media SDK 設定需要已設定 `visitor` 的 `AppMeasurement` 例項。

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. 設定 Media SDK

   每個網頁皆應設定 Media SDK 一次，且該設定將套用至所有已建立的 tracker 例項。

   >[!IMPORTANT]
   >
   > Media SDK (3.x) 使用媒體收集 API 來追蹤與 2.x SDK 中使用之 HB 端點不同的媒體。請聯絡您的 Adobe 代表取得更多資訊。

   以下示範 `MediaConfig` 初始化：

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. 建立 `MediaTracker` 例項。

   設定 Media SDK 後，可使用 `getInstance` API 建立追蹤媒體內容的 tracker 例項。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >請確保您的 `tracker` 例項可供存取，並且不會在媒體工作階段結束前遭到取消配置。此例項將用於為該工作階段追蹤下列所有事件。

## 從 JavaScript 2.x 移轉至 3.x

如需有關從 2.x 移轉至 3.x 的詳細資訊，請參閱[從 2.x 移轉至 3.x](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)。
