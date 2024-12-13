---
title: 瞭解Adobe串流媒體收集的先決條件
description: 開始使用串流媒體收集。 瞭解實作所需的專案。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 64%

---

# 先決條件 {#prerequisites}

開始實作Adobe串流媒體收集之前，請完成以下工作：

1. **檢閱串流媒體集合概觀**<br>
開始實作串流媒體收集之前，請先檢閱[串流媒體收集概觀](/help/media-overview.md)，確認它符合您的需求。

1. **確認您的定價模式**<br>
Adobe串流媒體收集附加元件目前的定價模型是以視訊串流為基礎。 如有必要，請聯絡您的銷售代表或Adobe客戶團隊，因為此附加元件是針對Adobe Analytics和Adobe Experience Platform分開銷售。

1. **啟用Adobe Analytics報表**<br>
若要在Analytics或Customer Journey Analytics中啟用報表，以及檢視您正在收集的內容和廣告資料，您必須啟用報表。 請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。

1. **在 Experience Cloud 中實作 Adobe Experience Platform 身分識別服務**

   **身分服務**&#x200B;可為 Experience Cloud 核心服務、解決方案以及 People 核心服務的客戶屬性和客群啟用共同的身分識別架構。其運用方式為指派一個唯一的永久性 ID 給網站訪客。當您的組織實作 ID 服務時，此 ID 可讓您在不同的 Experience Cloud 解決方案中識別相同的網站訪客及其資料。

   ![ID 服務圖形](assets/mc_id_service_graphic.png)

   ID 服務也可以取代不同的解決方案特定 ID (例如 Analytics AID)。透過[客戶 ID 和驗證狀態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hant)功能，ID 服務可讓您將您的客戶 ID 傳遞至 Experience Cloud。請記住，ID 服務僅適用於您已訂閱的解決方案。如果您未註冊存取其他產品，則 ID 服務不提供存取權。

   ID 服務是許多 Experience Cloud 特色、增強功能與服務的必要元件。目前 ID 服務支援 [Analytics](https://www.adobe.com/tw/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/tw/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/tw/marketing-cloud/testing-targeting.html)。

   如果您尚未實作 ID 服務，現在就是開始考慮移轉策略的最佳時機。如需 ID 服務之重要性和角色的詳細資訊，請參閱[為何您應認真考慮 Identity 服務](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

   如需 Experience Cloud ID 的詳細資訊，請參閱 [Experience Cloud ID 服務概觀](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。

1. **檢視您的實作的其他先決條件**

   根據您計畫實作串流媒體收集的方式，檢視下列任一實作方法的先決條件：

   * [僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Edge 實作的先決條件](/help/implementation/edge/prerequisites-edge.md)

   使用[實施概觀](/help/implementation/overview.md)以確定哪種實施方法適合您。
