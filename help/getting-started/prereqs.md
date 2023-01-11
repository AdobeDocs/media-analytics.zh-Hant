---
title: 了解串流媒體的先決條件
description: 開始使用適用於串流媒體的 Adobe Analytics。 了解實作適用於串流媒體的 Adobe Analytics 需要哪些條件。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: ht
source-wordcount: '486'
ht-degree: 100%

---

# 先決條件{#prerequisites}

要實作適用於串流媒體的 Adobe Analytics，請完成以下任務：

1. **確認您的串流媒體定價模式**<br>
目前的定價模型是以視訊串流為基礎。如有必要，請聯絡您的銷售代表或客戶經理以簽署新的銷售訂單，因為適用於串流媒體的 Analytics 與 Adobe Analytics 是分開銷售。

1. **確認您正在實作 Adobe Analytics**<br>
Adobe Analytics 適用的串流媒體還需要 Adobe Analytics 基本實作。請參閱[實作 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant)以取得詳細資訊。

1. **取得媒體追蹤伺服器 URL**<br>
請向您的 Adobe Analytics 代表詢問媒體追蹤伺服器 URL。這是 
`collection-api-server` URL，適用於 Mobile SDK、JavaScript SDK 和 Roku 的非 Collection API 追蹤伺服器。API 實作的網域名稱是：`[your_namespace].hb-api.omtrdc.net`。

1. **下載目前的 Media SDK 或實作必要的擴充功能**<br>
根據實作路徑，針對 Web、行動或過頂平台[下載目前的 SDK](download-sdks.md)。必須實作必要的擴充功能才能啟用適用於串流媒體的 Adobe Analytics 擴充功能路徑。

1. **啟用 Adobe Analytics 報表**<br>
要在 Analytics 中啟用報表並檢視您正在收集的內容和廣告資料，您必須在 Analytics 中啟用報表。請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。

1. **啟用 Experience Cloud**<br>


## 實作 Adobe Experience Platform Identity Service. {#implement-id}

**Identity 服務**&#x200B;可為 Experience Cloud 核心服務、解決方案以及 People 核心服務的客戶屬性和對象啟用共同的識別架構。其運用方式為指派一個唯一的永久性 ID 給網站訪客。當您的組織實作 ID 服務時，此 ID 可讓您在不同的 Experience Cloud 解決方案中識別相同的網站訪客及其資料。

![ID 服務圖形](assets/mc_id_service_graphic.png)

ID 服務也可以取代不同的解決方案特定 ID (例如 Analytics AID)。透過[客戶 ID 和驗證狀態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hant)功能，ID 服務可讓您將您的客戶 ID 傳遞至 Experience Cloud。請記住，ID 服務僅適用於您已訂閱的解決方案。如果您未註冊存取其他產品，則 ID 服務不提供存取權。

ID 服務是許多 Experience Cloud 特色、增強功能與服務的必要元件。目前 ID 服務支援 [Analytics](https://www.adobe.com/tw/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/tw/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/tw/marketing-cloud/testing-targeting.html)。

如果您尚未實作 ID 服務，現在就是開始考慮移轉策略的最佳時機。如需 ID 服務之重要性和角色的詳細資訊，請參閱[為何您應認真考慮 Identity 服務](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

如需 Experience Cloud ID 的詳細資訊，請參閱 [Experience Cloud ID 服務概觀](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。
