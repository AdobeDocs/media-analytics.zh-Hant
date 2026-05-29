---
title: 如何設定適用於串流媒體的 Analytics 的 Web 實作
description: 了解如何為 Web 應用程式實作 Adobe Streaming Media。
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 78%

---

# 使用JavaScript安裝Media SDK {#install-web-sdks}

>[!IMPORTANT]
>
>本頁涵蓋僅限Analytics的JavaScript Web SDK實作。 如需建議的實作，請參閱[使用Edge Network實作串流媒體](/help/implementation/edge/edge-web-sdk.md)。

本頁資訊說明如何安裝獨立 Web SDK 和設定 JavaScript。

或者，您可以使用Adobe Media Analytics擴充功能來實作串流媒體服務，如[使用Media Analytics擴充功能安裝串流媒體服務](/help/implementation/media-sdk/setup/web-implementation-tags.md)中所述。

## 先決條件 {#prerequesites}

* **取得有效設定參數**

  設定 Analytics 帳戶之後，可以向 Adobe 代表取得這些參數。

* **在您的媒體應用程式中實作 JavaScript 適用的 `AppMeasurement` 和 `Experience Cloud Identity Service`**

  如需詳細資訊，請參閱[使用JavaScript實作Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant)和使用AppMeasurement的[訪客身分識別](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/id/appmeasurement)。

* **在您的媒體播放器中包含以下 API**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 這包含目前播放的媒體、廣告和章節之相關資訊。

## 設定 JavaScript 3.x {#set-up-javascript}

1. 將[下載的](/help/getting-started/download-sdks.md)程式庫新增至專案。 為方便起見，請建立類別的本機參照。

   1. 展開您下載的 `MediaSDK-js-v3*.zip` 檔案。
   1. 驗證 `libs` 目錄中存在 `MediaSDK.js` 檔案。

   1. 主控 `MediaSDK.js` 檔案。

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。 下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.js`

      在每一頁的 `<head>` 或 `<body>` 標籤中新增下列程式碼行，加入 JavaScript 適用的 `MediaSDK`。 例如：

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
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. 設定 Media SDK

   每個網頁皆應設定 Media SDK 一次，且該設定將套用至所有已建立的 tracker 例項。

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
   >請確保您的 `tracker` 例項可供存取，並且不會在媒體工作階段結束前遭到取消配置。 此例項將用於為該工作階段追蹤下列所有事件。

## 從 JavaScript 2.x 移轉至 3.x

如需有關從2.x移轉至3.x的詳細資訊，請參閱[從JS SDK 2.x移轉至3.x](/help/implementation/media-sdk/setup/migrate-js-2x-to-3x.md)。
