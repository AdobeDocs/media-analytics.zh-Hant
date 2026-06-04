---
title: 設定適用於串流媒體的JavaScript
description: 安裝並設定適用於JavaScript (3.x)的Media SDK，用於僅限Analytics的串流媒體實作。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# 設定適用於串流媒體的JavaScript

適用於JavaScript的Media SDK (3.x)會將串流媒體資料直接傳送到Adobe Analytics。 本頁涵蓋手動JavaScript安裝。 若要改為透過標籤來部署SDK，請參閱[設定Media Analytics標籤擴充功能](javascript-tags.md)。 若為新實作，請考慮使用[網頁SDK](/help/implementation/edge/web-sdk.md)，透過Edge Network資料流傳送資料給Adobe Analytics。

* **必要條件**：
   * 完成[僅限Analytics的實作概觀](overview.md)。
   * 實作[AppMeasurement](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/js/overview)和[訪客ID服務](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement)。
   * [下載JavaScript的Media SDK](/help/getting-started/download-sdks.md)。

## 安裝和設定SDK

1. 主機`MediaSDK.js` （來自下載的`libs`目錄）位於所有網頁皆可存取的網頁伺服器上，並在每個網頁上參照該主機：

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. 每頁設定Media SDK一次，傳遞您設定為先決條件的`appMeasurement`執行個體：

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >`mediaConfig.trackingServer`變數是您的&#x200B;**媒體收集伺服器** （例如，`[namespace].hb-api.omtrdc.net`）。 此集合伺服器與AppMeasurement執行個體中設定的Analytics追蹤伺服器不同。

1. 建立具有`getInstance`的追蹤器執行個體。 讓執行個體在整個媒體工作階段中皆可存取：

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## 追蹤媒體事件

建立追蹤器後，請使用其追蹤器方法來追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Media SDK JS 3.x**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [適用於JavaScript 3.x API的Media SDK參考](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [從JS SDK 2.x移轉至3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [設定Media Analytics標籤擴充功能](javascript-tags.md)
>* [事件總覽](/help/implementation/events/overview.md)
