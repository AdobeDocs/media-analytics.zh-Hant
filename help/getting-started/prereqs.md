---
title: 了解串流媒體的先決條件
description: 開始使用適用於串流媒體的 Adobe Analytics。 了解實施適用於串流媒體的 Adobe Analytics 需要哪些條件。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# 先決條件{#prerequisites}

若要實作適用於串流媒體的Adobe Analytics，請完成下列工作：

1. **確認您的Stiming Media定價模型**<br>
目前的定價模式是以視訊資料流為基礎。 如有需要，請連絡您的銷售代表或客戶經理以簽署新的銷售訂單，因為Streaming Media Analytics與Adobe Analytics分開銷售。

1. **確認您正在實作Adobe Analytics**<br>
Adobe Analytics適用的串流媒體也需要Adobe Analytics基本實作。 請參閱 [實作Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) 以取得更多資訊。

1. **取得媒體追蹤伺服器URL**<br>
請洽詢您的Adobe Analytics代表以取得媒體追蹤伺服器URL。 這是 
`collection-api-server` 行動SDK的URL、JavaScript SDK以及Roku的非收集API追蹤伺服器。 API實作的網域名稱為： `[your_namespace].hb-api.omtrdc.net`.

1. **下載最新的Media SDK或實作必要的擴充功能**<br>
視實作路徑而定， [下載目前的SDK](download-sdks.md) 適用於網頁、行動或頂端平台。 必須實作必要的擴充功能，才能啟用Adobe Analytics for Streaming Media。 如需必要擴充功能的相關資訊，請參閱 [Adobe擴充功能](download-sdks.md#media-extension). （需要釐清下載Media SDK或取得擴充功能）

1. **啟用Adobe Analytics報表**<br>
若要在Analytics中啟用報表以及檢視您要收集的內容和廣告資料，您必須在Analytics中啟用報表。 請參閱 [啟用媒體報表。](/help/reporting/media-reports-enable.md).

1. **啟用Experience Cloud**<br>


## 實施 Adobe Experience Platform Identity Service. {#implement-id}

此 **Identity服務** 為Experience Cloud核心服務、解決方案以及People核心服務中的客戶屬性和觀眾啟用共同識別架構。 其運用方式為指派一個唯一的永久性 ID 給網站訪客。當您的組織實施 ID 服務時，此 ID 可讓您在不同的 Experience Cloud 解決方案中識別相同的網站訪客及其資料。

![ID服務圖](assets/mc_id_service_graphic.png)

ID 服務也可以取代不同的解決方案特定 ID (例如 Analytics AID)。透過[客戶 ID 和驗證狀態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hant)功能，ID 服務可讓您將您的客戶 ID 傳遞至 Experience Cloud。請記住，ID 服務僅適用於您已訂閱的解決方案。如果您未註冊存取其他產品，則 ID 服務不提供存取權。

ID服務是許多Experience Cloud功能、增強功能和服務的必要元件。 目前 ID 服務支援 [Analytics](https://www.adobe.com/tw/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/tw/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/tw/marketing-cloud/testing-targeting.html)。

如果您尚未實施 ID 服務，現在就是開始考慮移轉策略的最佳時機。如需 ID 服務之重要性和角色的詳細資訊，請參閱[為何您應認真考慮 Identity 服務](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

如需 Experience Cloud ID 的詳細資訊，請參閱 [Experience Cloud ID 服務總覽](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。
