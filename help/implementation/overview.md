---
title: 實作串流媒體收集
description: 瞭解串流媒體收集的實作路徑。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 69%

---

# 實作串流媒體收集

有多種方式可實施Adobe串流媒體收集。 有關本頁描述的實施方法所支援的裝置和平台的詳細比較，請參閱[支援的裝置和平台](/help/getting-started/supported-devices.md)。

## Edge 實施方法

我們建議為所有新Adobe Analytics或Customer Journey Analytics客戶實作串流媒體收集時使用Edge。

* **用於Edge NetworkSDK /擴充功能的媒體：**&#x200B;從網頁、iOS和Android裝置或Roku裝置收集資料，並傳送給Edge Network。 之後可將資料傳送至 Customer Journey Analytics 或 Adobe Analytics。

  如需Edge NetworkSDK /擴充功能所用媒體的詳細資訊，請參閱[使用Edge Network實作串流媒體收集](/help/implementation/edge/implementation-edge.md)。

* **Media Edge API：**&#x200B;可自訂為從任何裝置或格式（包括行動裝置、網頁和過頂裝置）收集資料，並將資料傳送至Edge Network。 之後可將資料傳送至 Customer Journey Analytics 或 Adobe Analytics。

  如需Media Edge API的詳細資訊，請參閱[Media Edge API總覽](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/)。

![CJA 工作流程](assets/streaming-media-edge.png)

## 僅限 Adobe Analytics 的實施方法

建議將上述 Edge 實施方法用於 Customer Journey Analytics 和 Adobe Analytics，特別是對於新實施。

除了 Edge 實施方法之外，還有其他實施方法。 這些實施方法專為與 Adobe Analytics 搭配使用而設計。 但是，採用以下任何實施方法的現有客戶仍然可以透過建立 [Analytics 來源連線](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=zh-Hant)的方式，使資料可用於 Customer Journey Analytics。

* **含標記的 Media 擴充功能：** Adobe Media Analytics for Audio and Video 擴充功能提供了將 Media 追蹤器例項新增到啟用標記的網站或專案的功能。資料會傳送至 Adobe Analytics。

  如需安裝、設定和實作含標記的 Media 擴充功能的相關資訊，請參閱[Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能概觀](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=zh-Hant)。

* **Media SDK：** Media SDK 可讓您測量多種媒體平台，包括網站、手機、連網電視、平板電腦、OTT 裝置、機上盒和遊戲主機。(如需詳細資訊，請參閱[支援的裝置和平台](/help/getting-started/supported-devices.md)。)

  Media SDK 使用 Media Collection API 進行追蹤。資料會傳送至 Adobe Analytics。

  如需有關下載和安裝 Media SDK 和擴充功能的資訊，請參閱[取得 Media SDK、使用標記的擴充功能和 OTT SDK](/help/getting-started/download-sdks.md)。

* **Media Collection API：**&#x200B;由於 Media Collection API 是可自訂的，因此它們可用於需要自訂追蹤功能的應用程式以及 Media SDK 不支援的裝置。Media Collection API 使用 RESTful HTTP 呼叫追蹤音訊和視訊事件。資料會傳送至 Adobe Analytics。

  如需關於使用 Media Collection API 的資訊，請參閱 [Media Collection API](media-collection-api/mc-api-overview.md)。


![Analytics 工作流程](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
