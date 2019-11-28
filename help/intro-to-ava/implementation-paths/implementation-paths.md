---
title: 實施路徑
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 實施路徑 {#implementation-paths}

Media Analytics (心率) 是 Adobe 的標準化媒體解決方案。它已經取代 Adobe 的舊版里程碑模型。

關於這些實施路徑，客戶需要聯絡他們的銷售代表/客戶經理以簽署新的銷售訂單，因為 Media Analytics 具有獨特的 SKU，並且從基於伺服器呼叫的定價模式變更為基於視訊資料流的模式。

* **用戶端 -** 它們是僅限 Media Analytics 的整合。您可以選擇視訊心率 SDK 與/或媒體收集 API 整合。此路徑可用於任何視訊播放器，包括客戶及/或 OVP 播放器，例如 Brightcove、Ooyala、thePlatform 等。

   如果 Media Analytics 是您打算使用的路徑，請參閱 [Media SDK 實施](/help/sdk-implement/setup/setup-overview.md)與[媒體收集 API](/help/media-collection-api/mc-api-overview.md)。

   >[!IMPORTANT]
   >
   >若要使用 Media Analytics，客戶也必須使用 Adobe Analytics。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch 是 Dynamic Tag Management 的後續產品，能提供 Media Analytics Launch 擴充功能來協助您在播放器中實作視訊追蹤。

   您可以在這裡深入瞭解 Experience Platform Launch: [Adobe Media Analytics for Audio and Video 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime -** Adobe Primetime 是 Adobe Experience Cloud 解決方案，可幫助內容程式設計師和經銷商在每個連線的畫面上透過媒體獲利。

   Primetime 藉由提供模組化平台以進行視訊發佈、廣告刊登、個人化和分析，消除了各裝置之間的可及範圍、創造營收和啟動全域對象的複雜性。此外，Primetime 也提供了以下解決方案和值:

   * 支援準確測量線性和 VOD 內容類型。
   * 支援評量包含 (或不包含) 動態廣告插入的廣告插播。
   * TVSDK 的流暢廣告插入模型允許直接測量廣告播放的分析，進而提高準確性。
   * 強大的事件和中繼資料集合，可確保跨 QoS 緩衝或行動連線中斷問題以一般使用者互動 (例如在行動裝置上搜尋、暫停和後台處理) 的準確性。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK 已與 Media Analtyics (心率) SDK 整合，使得在每個支援的平台上實作時更加簡單快速。<!--Primetime also supports the partnership with Nielsen.-->若要利用 Primetime，請遵循在以下內容中找到的相同指引和必要條件: [用戶端](/help/intro-to-ava/implementation-paths/client-side-path.md)以及適用於您平台的下列文件: [Primetime 使用手冊](https://helpx.adobe.com/tw/primetime/user-guide.html)。

您也應該聯絡銷售代表/客戶經理，討論購買 TVSDK 的所需作業。
