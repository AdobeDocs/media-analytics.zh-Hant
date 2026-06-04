---
title: 設定適用於串流媒體的Web SDK
description: 設定Adobe Experience Platform Web SDK (alloy.js)，將串流媒體資料傳送至Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# 設定適用於串流媒體的Web SDK

Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview) （`alloy.js`，版本2.20.0或更新版本）的`streamingMedia`元件會收集您網站上的媒體工作階段資料，並將其傳送至Edge Network。 本頁涵蓋程式碼內(`alloy.js`)設定。 若要改為透過標籤設定網頁SDK，請參閱[為串流媒體設定網頁SDK標籤擴充功能](web-sdk-tags.md)。

* **必要條件**：
   * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
   * 安裝Web SDK 2.20.0或更新版本。 請參閱[安裝網頁SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview)。

## 設定streamingMedia元件

將`streamingMedia`元件新增至您的`alloy`設定：

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

如需完整的組態詳細資料，請參閱[`streamingMedia`命令](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)。

### 從Media JS SDK移轉

如果您從Media JS (3.x) SDK移動，Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker)命令會傳回與[3.x Media SDK](/help/implementation/analytics-only/javascript.md)相同API的追蹤器執行個體，因此您現有的追蹤呼叫可繼續運作。

## 追蹤媒體事件

設定SDK後，呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)以傳送每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**網頁SDK**&#x200B;標籤，以取得確切的裝載。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [Web SDK 概觀](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
