---
title: 快速入門
description: 開始使用Adobe Analytics for Streaming Media。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# 快速入門 {#getting-started}

Adobe Analytics for Streaming Media提供兩種主要實作方法： Media SDK和Media Collection API。

![方法](assets/getting-started2.png)

使用 **Media SDK**，您可以精確測量多個媒體平台，包括網站、行動電話、連線電視、平板電腦、OTT裝置、機上盒及遊戲主機。 您甚至可以測量下載的內容。 深入了解使用者檢視參與度的深入分析，以便您了解檢視者參與的時間、時間和位置。 Media SDK會使用 **媒體收集API** ，以追蹤。 如果您的應用程式需要自訂追蹤功能，則可自訂媒體收集API。 若為Media SDK不支援的裝置，您可以使用媒體收集API。

Adobe Analytics串流媒體解決方案適用於下列媒體平台：

* Web
* 行動
* 超越
* 可用於串流媒體或伺服器對伺服器整合的任何連接設備

如需詳細資訊，請參閱 [支援的裝置和平台](#_Supported_devices_and).

>[!IMPORTANT]
>
>若要實作Adobe Analytics串流媒體，請連絡您的Adobe銷售代表或客戶經理，確認串流媒體是您產品組合的一部分。

## 適用於串流媒體的Media SDK {#media-sdks}

串流媒體適用的Media SDK適用於JavaScript、Android、iOS、tvOS、Chromecast和Roku平台。

如需下載和安裝Media SDK的詳細資訊，請參閱 [取得Media SDK、使用標籤的擴充功能，以及OTT SDK](/help/getting-started/download-sdks.md).


## 媒體收集API {#media-collection-apis}

此 **媒體收集API** 可讓您自訂您的media analytics實作。 使用媒體收集API直接呼叫Adobe的伺服器，以執行幾乎所有可透過SDK執行的動作，以及執行其他動作。 自訂資料收集，以建立可探索、獲得深入分析或回答有關串流媒體資料之重要問題的報表。

如需使用媒體收集API的詳細資訊，請參閱 [Stemid Media API檔案](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe 擴充功能 {#adobe-extensions}

>[!NOTE]
>
>需要擴充功能的簡介

* 此 [**Adobe MediumAnalytics for Audio and Video擴充功能**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) （Media Analytics擴充功能），是iOS和tvOS實作的必要功能。 它提供將追蹤器例項新增至標籤網站或專案的功能。 MA擴充功能也需要Analytics擴充功能和Experience CloudID擴充功能。

* [Analytics擴充功能v1.6或更新版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en) — 此擴充功能可讓您載入Adobe Experience Platform Web SDK Javascript程式庫，以傳送資料至Adobe解決方案。

* [Experience CloudID擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en) — 此擴充功能實作Experience CloudID服務，可識別所有Experience Cloud解決方案中的訪客。 Experience CloudID服務是Adobe Experience Platform中的個人化擴充功能。
