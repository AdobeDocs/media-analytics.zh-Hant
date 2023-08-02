---
title: 了解串流媒體的先決條件
description: 開始使用適用於串流媒體的 Adobe Analytics。 了解實作適用於串流媒體的 Adobe Analytics 需要哪些條件。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 92%

---

# 先決條件 {#prerequisites}

在開始實作串流媒體之前，請完成以下任務：

1. **檢閱串流媒體概觀**<br>
在開始實作串流媒體之前，請檢閱[串流媒體概觀](/help/media-overview.md)，以確保串流媒體滿足您的需求。

1. **確認您的串流媒體定價模式**<br>
目前的定價模型是以視訊串流為基礎。如有必要，請聯絡您的銷售代表或Adobe客戶團隊，因為串流媒體是作為Adobe Analytics的附加元件另外銷售。<!--update when media SKUs are added to other AEP apps -->

1. **啟用 Adobe Analytics 報表**<br>
要在 Analytics 中啟用報表並檢視您正在收集的內容和廣告資料，您必須在 Analytics 中啟用報表。請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。

1. **在 Experience Cloud 中實作 Adobe Experience Platform 身分識別服務**

   **Identity 服務**&#x200B;可為 Experience Cloud 核心服務、解決方案以及 People 核心服務的客戶屬性和對象啟用共同的識別架構。其運用方式為指派一個唯一的永久性 ID 給網站訪客。當您的組織實作 ID 服務時，此 ID 可讓您在不同的 Experience Cloud 解決方案中識別相同的網站訪客及其資料。

   ![ID 服務圖形](assets/mc_id_service_graphic.png)

   ID 服務也可以取代不同的解決方案特定 ID (例如 Analytics AID)。透過[客戶 ID 和驗證狀態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hant)功能，ID 服務可讓您將您的客戶 ID 傳遞至 Experience Cloud。請記住，ID 服務僅適用於您已訂閱的解決方案。如果您未註冊存取其他產品，則 ID 服務不提供存取權。

   ID 服務是許多 Experience Cloud 特色、增強功能與服務的必要元件。目前 ID 服務支援 [Analytics](https://www.adobe.com/tw/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/tw/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/tw/marketing-cloud/testing-targeting.html)。

   如果您尚未實作 ID 服務，現在就是開始考慮移轉策略的最佳時機。如需 ID 服務之重要性和角色的詳細資訊，請參閱[為何您應認真考慮 Identity 服務](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

   如需 Experience Cloud ID 的詳細資訊，請參閱 [Experience Cloud ID 服務概觀](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。

1. **檢視您的實作的其他先決條件**

   依據您計劃如何實作串流媒體，檢視以下任一實作方法的先決條件：

   * [僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Edge 實作的先決條件](/help/implementation/edge/prerequisites-edge.md)

   使用 [實施概述](/help/implementation/overview.md) 以判斷適合您的實作方法。
