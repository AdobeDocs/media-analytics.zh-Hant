---
title: 必備條件
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 必備條件{#prerequisites}

## 決策 {#decision}

在開始實作追蹤前，請先決定與您的情況最為相關的實作：

* **Media Analytics -** 使用最新 Media SDK (標準建議實作) 及/或媒體收集 API (RESTful)
* **里程碑 -** 舊版 Adobe 追蹤實作
* **Data Insertion API -** 不使用 Media SDK 實作追蹤

## 工作 {#prereq-tasks}

對於 *Media Analytics* 實作，您必須先完成下列工作：

1. **啟用 Experience Cloud。**

   您需要實作Adobe Experience Platform Identity Service。

    Identity 服務可為 Experience Cloud 核心服務、解決方案以及 People 核心服務的客戶屬性和觀眾啟用共同識別架構。其運用方式為指派一個唯一的永久性 ID 給網站訪客。當您的組織實施 ID 服務時，此 ID 可讓您在不同的 Experience Cloud 解決方案中識別相同的網站訪客及其資料。

   ![](assets/mc_id_service_graphic.png)

   ID 服務也可以取代不同的解決方案特定 ID (例如，Analytics AID)。透過[客戶 ID 和驗證狀態](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html)功能，ID 服務可讓您將您的客戶 ID 傳遞至 Experience Cloud。請記住，ID 服務僅適用於您已訂閱的解決方案。如果您未註冊存取其他產品，則 ID 服務不提供存取權。

   展望未來，ID 服務將成為許多目前與未來 Experience Cloud 特色、增強功能與服務的必要元件。Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >若要參與Adobe Experience Cloud Device Co-op，必須有Experience Cloud ID服務。

   如果您尚未實施 ID 服務，現在就是開始考慮移轉策略的最佳時機。For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **啟用 Adobe Analytics 報表。**

   To enable reports in Analytics and see the content and ad data you are collecting, see [Media reports enablement.](/help/media-reports/media-reports-enable.md)

