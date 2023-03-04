---
title: 有哪些串流媒體實作路徑可以使用？
description: 了解 Adobe 串流媒體實作路徑，包括 Adobe Experience Platform 資料收集。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0c1382c9c4f1488fba81575097d154301a9b8e70
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 93%

---

# 實作路徑 {#implementation-paths}

**此內容已移至目前實作路徑檔案**

對於每個實作路徑，客戶都需要聯絡其銷售代表/Adobe客戶團隊以簽署新的銷售訂單，因為Streaming Media Analytics具有獨特的SKU，並且從基於伺服器呼叫的定價模式變更為基於視訊資料流的模式。

## 具有 Adobe Media Analytics 擴充功能的 Adobe Experience Platform 資料收集

>[!NOTE]
>Adobe Experience Platform Launch 已經過品牌重塑，現在是 Experience Platform 中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-Hant)。


Adobe Experience Platform 標記是新一代 Adobe 標記管理功能。標記可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標記功能，以強化相關客戶體驗。標記以隨附的加值功能形式提供給 Adobe Experience Cloud 客戶。

標記可讓任何人建置和維護自己的整合，稱為擴充功能。這些擴充功能為 Adobe Experience Cloud 客戶提供應用程式商店的使用體驗，讓客戶快速安裝、設定和部署自己的標記。

擴充功能是可擴充標記功能的程式碼 (JavaScript、HTML 及 CSS) 套件。使用幾乎為自助服務的介面來建置、管理和更新您的整合。您可以將擴充功能視為用來完成工作的應用程式。如需詳細資訊，請參閱 [Adobe Experience Platform 文件](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hant)中的&#x200B;*標記概觀*&#x200B;文章

Adobe Media Analytics (MA) 擴充功能新增了音訊和視訊的核心 JavaScript Media SDK (Media 2.x SDK)。此擴充功能可將 `MediaHeartbeat` 追蹤器例項新增至資料收集網站或專案。

Adobe Data Collection 搭配 Media Analytics 擴充功能使用，須符合以下條件：
* 您必須是 Adobe Experience Cloud 客戶。
* 您必須在網頁上部署資料收集或 DTM 內嵌程式碼。
* [Analytics 擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hant)
* [Experience Cloud ID 擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh=Hant)


## 用戶端

這些是僅限 Media Analytics 的整合。您可以選擇視訊心率 SDK 與/或 Media Collection API 整合。此路徑可用於任何視訊播放器，包括客戶及/或 OVP 播放器，例如 Brightcove、Ooyala、thePlatform 等。

如果 Media Analytics 是您打算使用的路徑，請參閱 [Media SDK 實作](/help/legacy/setup/legacy-setup-overview.md)與 [Media Collection API](/help/implementation/media-collection-api/mc-api-overview.md)。

>[!IMPORTANT]
>若要使用 Media Analytics，客戶也必須使用 Adobe Analytics。

## Adobe Primetime

Adobe Primetime 是 Adobe Experience Cloud 解決方案，可幫助內容程式設計師和經銷商在每個連通螢幕上透過媒體獲利。

Primetime 藉由提供模組化平台以進行視訊發佈、廣告刊登、個人化和分析，消除了各裝置之間的可及範圍、創造營收和啟動全域對象的複雜性。此外，Primetime 也提供了以下解決方案和值：

* 支援準確測量線性和 VOD 內容類型。
* 支援測量包含 (或不包含) 動態廣告插入的廣告插播。
* TVSDK 的流暢廣告插入模型允許直接測量廣告播放的分析，進而提高準確性。
* 強大的事件和中繼資料集合，可確保跨 QoS 緩衝或行動連線中斷問題以及一般使用者互動 (例如在行動裝置上搜尋、暫停和背景處理) 的準確性。
* Nielsen DTVR (線性) 與 ID3 中繼資料以及 DCR 與 CMS 中繼資料的整合支援。


TVSDK 已與 Media Analtyics (心率) SDK 整合，使得在每個支援的平台上實作時更加簡單快速。若要妥善運用 Primetime，請遵循適用於[用戶端](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md)的同一套準則和先決條件，並根據您所使用的平台參閱相對應的 [Primetime 使用手冊](https://helpx.adobe.com/tw/primetime/user-guide.html)。

您也應該聯絡銷售代表/客戶經理，討論購買 TVSDK 的所需作業。
