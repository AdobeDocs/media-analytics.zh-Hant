---
title: 實作適用於串流媒體的 Adobe Analytics 或 Customer Journey Analytics
description: 了解串流媒體實作路徑。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 81%

---

# 實作適用於串流媒體的 Adobe Analytics 或 Customer Journey Analytics

實作串流媒體的方法有很多種。 有關本頁描述的實施方法所支援的裝置和平台的詳細比較，請參閱[支援的裝置和平台](/help/getting-started/supported-devices.md)。

## Edge 實施方法

我們建議在為所有 Adobe Analytics 或 Customer Journey Analytics 新客戶實作媒體分析時使用 Edge。

* **Media for Edge Network SDK/擴充功能：**&#x200B;從 iOS 和 Android 裝置收集資料並傳送至 Edge。 之後可將資料傳送至 Customer Journey Analytics 或 Adobe Analytics。

  如需 Media for Edge Network SDK/擴充功能的詳細資訊，請參閱[使用 Experience Platform Edge 安裝 Media Analytics](/help/implementation/edge/implementation-edge.md)。

  >[!NOTE]
  >
  >此實施方式目前不支援 Web SDK 或 Roku。 但是，當使用 Media Edge API 實作時，兩者均受支援。

* **Media Edge API：**&#x200B;可以進行自訂，收集任何裝置或格式 (包括行動、網路和 OTT 裝置) 的資料並將資料傳送至 Edge。之後可將資料傳送至 Customer Journey Analytics 或 Adobe Analytics。

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA 工作流程](assets/cja-implementation.png)

## 僅限 Adobe Analytics 的實施方法

建議將上述 Edge 實施方法用於 Customer Journey Analytics 和 Adobe Analytics，特別是對於新實施。

除了 Edge 實施方法之外，還有其他實施方法。 這些實施方法專為與 Adobe Analytics 搭配使用而設計。 但是，採用以下任何實施方法的現有客戶仍然可以透過建立 [Analytics 來源連線](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=zh-Hant)的方式，使資料可用於 Customer Journey Analytics。

* **含標記的 Media 擴充功能：** Adobe Media Analytics for Audio and Video 擴充功能提供了將 Media 追蹤器例項新增到啟用標記的網站或專案的功能。資料會傳送至 Adobe Analytics。

  如需安裝、設定和實作含標記的 Media 擴充功能的相關資訊，請參閱[Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能概觀](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html)。

* **Media SDK：**  Media SDK可讓您測量多種媒體平台，包括網站、手機、連線電視、平板電腦、OTT裝置、機上盒和遊戲主機。 (如需詳細資訊，請參閱 [支援的裝置和平台](/help/getting-started/supported-devices.md).)

  Media SDK使用Media Collection API進行追蹤。 資料會傳送至 Adobe Analytics。

  如需有關下載和安裝 Media SDK 和擴充功能的資訊，請參閱[取得 Media SDK、使用標記的擴充功能和 OTT SDK](/help/getting-started/download-sdks.md)。

* **Media Collection API：** 由於Media Collection API可自訂，因此可用於需要自訂追蹤功能的應用程式及Media SDK不支援的裝置。 Media Collection API使用RESTful HTTP呼叫來追蹤音訊和視訊事件。 資料會傳送至 Adobe Analytics。

  如需關於使用 Media Collection API 的資訊，請參閱 [Media Collection API](media-collection-api/mc-api-overview.md)。


![Analytics 工作流程](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
