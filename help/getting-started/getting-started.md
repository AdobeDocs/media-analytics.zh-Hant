---
title: 快速入門
description: 適用於串流媒體的 Adobe Analytics 快速入門。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# 快速入門 {#getting-started}

適用於串流媒體的 Adobe Analytics 提供兩種主要的實施方法，Media SDK 和 Media Collection API。

![方法](assets/getting-started2.png) 

使用 **Media SDK** 的內建邏輯，您可以準確測量多種媒體平台，包括網站、手機、連線電視、平板電腦、OTT 裝置、機上盒和遊戲主機。您甚至可以測量下載的內容。您獲得的見解深入洞悉使用者觀看參與度，能讓您了解觀眾參與的時間長短、時間和地點。Media SDK 使用 **Media Collection API**&#x200B;進行追蹤。Media Collection API 可自訂，如果您的應用程式需要自訂追蹤功能的話。對於 Media SDK 不支援的裝置，您可以使用 Media Collection API。

Adobe Analytics 串流媒體解決方案適用於以下媒體平台：

* Web
* Mobile
* 過頂
* 任何可用於串流媒體或伺服器對伺服器整合的連結裝置

如需詳細資訊，請參閱[支援的裝置和平台](#_Supported_devices_and)。

>[!IMPORTANT]
>
>要實施 Adobe Analytics 串流媒體，請聯絡您的 Adobe 銷售代表或客戶經理，以確保串流媒體是您產品組合的一部分。

## 適用於串流媒體的 Media SDK {#media-sdks}

適用於串流媒體的 Media SDK 可供 JavaScript、Android、iOS、tvOS、Chromecast 和 Roku 平台使用。

如需關於下載和安裝媒體 SDK 的資訊，請參閱[取得 Media SDK、使用標記的擴充功能和 OTT SDK](/help/getting-started/download-sdks.md)。


## Media Collection API {#media-collection-apis}

**Media Collection API**&#x200B;允許您自訂媒體分析實施。使用 Media Collection API 直接呼叫 Adobe 的伺服器來執行幾乎所有您可以使用 SDK 執行的動作，以及其他動作。 自訂您的資料收集來建立報表，以探索、獲取見解或回答有關您的串流媒體資料的重要問題。

如需關於使用 Media Collection API 的資訊，請參閱[串流媒體 API 文件](/help/implementation/media-collection-api/mc-api-overview.md)。

## Adobe 擴充功能 {#adobe-extensions}

* iOS 和 tvOS 實施需要 [**Adobe Media Analytics for Audio and Video 擴充功能**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=zh-Hant) (Media Analytics 擴充功能)。它提供將追蹤器例項新增至標記網站或專案的功能。MA 擴充功能還需要 Analytics 擴充功能和 Experience Cloud ID 擴充功能。

* [Analytics 擴充功能 v1.6 或更高版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hant) — 此擴充功能允許您載入 Adobe Experience Platform Web SDK Javascript 程式庫，將資料傳送到 Adobe 解決方案。

* [Experience Cloud ID 擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh-Hant) — 此擴充功能實施 Experience Cloud ID 服務，該服務可識別所有 Experience Cloud 解決方案中的訪客。 Experience Cloud ID 服務是 Adobe Experience Platform 中的個人化擴充功能。
