---
title: 瞭解Adobe串流媒體服務的先決條件
description: 開始使用串流媒體服務。 瞭解實作所需的專案。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 489
ht-degree: 46%

---

# 先決條件 {#prerequisites}

開始實作Adobe串流媒體服務前，請先完成下列工作：

1. **檢閱Adobe串流媒體服務總覽**<br>
在您開始實作串流媒體服務之前，請先檢閱[Adobe串流媒體服務總覽](/help/media-overview.md)，確定它符合您的需求。

1. **確認您的定價模式**<br>
Customer Journey Analytics串流媒體收集附加元件和Adobe Analytics for Streaming Media附加元件目前的定價模型是以視訊串流為基礎。 如有必要，請聯絡您的銷售代表或Adobe客戶團隊，因為此附加元件是針對Adobe Analytics和Adobe Experience Platform分開銷售。

1. **啟用Adobe Analytics報表**<br>
若要在Analytics或Customer Journey Analytics中啟用報表，以及檢視您正在收集的內容和廣告資料，您必須啟用報表。 請參閱[啟用 Media 報表](/help/implementation/media-sdk/setup/media-reports-enable.md)。

1. **在CX Enterprise中實作Adobe Experience Platform Identity Service**

   **Identity服務**&#x200B;可為CX Enterprise核心服務、解決方案以及People核心服務的客戶屬性和對象啟用共同識別架構。 其運用方式為指派一個唯一的永久性 ID 給網站訪客。 當貴組織實作ID服務時，此ID可讓您在不同的CX Enterprise解決方案中識別相同的網站訪客及其資料。

   ![ID 服務圖形](assets/mc_id_service_graphic.png)

   ID 服務也可以取代不同的解決方案特定 ID (例如 Analytics AID)。 透過[客戶ID和驗證狀態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hant)功能，ID服務可讓您將您的客戶ID傳遞至CX Enterprise。 請記住，ID 服務僅適用於您已訂閱的解決方案。 如果您未註冊存取其他產品，則 ID 服務不提供存取權。

   ID服務是許多CX Enterprise功能、增強功能與服務的必要元件。 目前 ID 服務支援 [Analytics](https://www.adobe.com/tw/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/tw/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/tw/marketing-cloud/testing-targeting.html)。

   如果您尚未實作 ID 服務，現在就是開始考慮移轉策略的最佳時機。 如需 ID 服務之重要性和角色的詳細資訊，請參閱[為何您應認真考慮身分識別服務](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

   如需 Experience Cloud ID 的詳細資訊，請參閱 [Experience Cloud ID 服務概觀](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)和 [Adobe Experience Platform 身分識別服務](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。

1. **檢視您的實作的其他先決條件**

   根據您計畫實作串流媒體服務的方式，檢視下列任一實作方法的先決條件：

   * [僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Edge 實作的先決條件](/help/implementation/edge/prerequisites-edge.md)

   使用[實施概觀](/help/implementation/overview.md)以確定哪種實施方法適合您。
