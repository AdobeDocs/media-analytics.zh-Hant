---
title: 設定JavaScript 3.x
description: 在JavaScript 3.x上實作的媒體SDK應用程式設定。
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# 設定JavaScript 3.x{#set-up-javascript}

## 必備條件

* **取得有效的設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的媒`AppMeasurement`體應`Experience Cloud Identity Service`用程式中實作和**&#x200B;適用JavaScript如需詳細資訊，請參 [閱使用JavaScript實作Analytics](https://docs.adobe.com/content/help/zh-Hant/analytics/implementation/js/overview.html)[和實作Experience Cloud Identity Service。](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **在您的媒體播放器中提供下列功能：**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的API* —— 這包括目前播放媒體、廣告、章節的相關資訊。

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-3x-sdks)程式庫新增至專案。為方便起見，請建立類別的本機參照。

   1. 展開您下載的 `MediaSDK-js-v3*.zip` 檔案。
   1. 驗證 `MediaSDK.js` 目錄中存在 `libs` 檔案.

   1. 主控 `MediaSDK.js` 檔案。

      此核心 JavaScript 檔案必須放置您網站所有頁面都能存取的網站伺服器上。下一個步驟需要用到前往這些檔案的路徑。

   1. 在所有網站頁面上參考 `MediaSDK.js`

      在每一頁的 `<head>` 或 `<body>` 標籤中新增下列程式碼行，加入 JavaScript 適用的 `MediaSDK`。例如：

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. 要快速驗證庫是否已成功導入，請在Window對 `ADB.Media` 像上導出檢查。

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. 建立和設 `AppMeasurement` 定例項 `visitor`。

   Media SDK設定需要已設定 `AppMeasurement` 的例 `visitor` 項。

```js
var appMeasurement = new AppMeasurement(“<rsid>”);
appMeasurement.visitor = visitor;
appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
```

1. 設定媒體SDK

   Media SDK應依網頁設定一次，且組態會套用至所有建立的追蹤器例項。

   >[!IMPORTANT]
   >
   > Media SDK(3.x)使用Media Collection API來追蹤與2.x SDK中使用的HB端點不同的媒體。 請連絡您的Adobe代表以取得更多資訊。


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
   
1. 建立 `MediaTracker` 例項。

   在設定Media SDK後，可使用 `getInstance` API建立追蹤媒體內容的追蹤器例項。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >請確保您的 `tracker` 例項可供存取，並且不會在媒體工作階段結束前遭到取消配置。此例項將用於追蹤該作業的所有下列事件。

## 從JavaScript 2.x移轉至3.x

如需有關從 2.x 移轉至 3.x 的詳細資訊，請參閱[從 2.x 移轉至 3.x](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)。
