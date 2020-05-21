---
title: 實施路徑
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---


# 實施路徑 {#implementation-paths}

對於每個實作路徑，客戶都需要聯絡其銷售代表／客戶經理以簽署新的銷售訂單，因為Media Analytics有唯一的SKU，並且從根據伺服器呼叫的定價模型變更為基於視訊串流的模型。

* **Adobe Launch搭配Adobe Media Analytics擴充功能**

   Adobe Launch是Adobe的新一代標籤管理解決方案。 Launch提供簡單的方式，來部署和管理所有必要的分析、行銷和廣告標籤，以推動相關的客戶體驗。 若要建立並維護您與Launch的整合，請使用擴充功能。 副檔名是JavaScript、HTML和CSS套件，可擴充Launch UI和用戶端功能。 如需詳細資訊，請參閱 [Experience Platform Launch使用指南](https://docs.adobe.com/content/help/zh-Hant/launch/using/overview.html)

   Adobe Media Analytics(MA)擴充功能新增了音訊和視訊的核心JavaScript Media SDK(Media 2.x SDK)。 此擴充功能提供將 `MediaHeartbeat` 追蹤器例項新增至 Launch 網站或專案的功能。

   Adobe Launch搭配Media Analytics擴充功能需要：
   * 您必須是Adobe Experience Cloud客戶。
   * 您必須在網頁上部署Launch或DTM內嵌代碼。
   * [Analytics 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **用戶端 -** 它們是僅限 Media Analytics 的整合。您可以選擇視訊心率 SDK 與/或媒體收集 API 整合。此路徑可用於任何視訊播放器，包括客戶及/或 OVP 播放器，例如 Brightcove、Ooyala、thePlatform 等。

   如果 Media Analytics 是您打算使用的路徑，請參閱 [Media SDK 實施](/help/sdk-implement/setup/setup-overview.md)與[媒體收集 API](/help/media-collection-api/mc-api-overview.md)。

   >[!IMPORTANT]
   >
   >若要使用 Media Analytics，客戶也必須使用 Adobe Analytics。

* **Adobe Primetime -** Adobe Primetime 是 Adobe Experience Cloud 解決方案，可幫助內容程式設計師和經銷商在每個連線的畫面上透過媒體獲利。

   Primetime 藉由提供模組化平台以進行視訊發佈、廣告刊登、個人化和分析，消除了各裝置之間的可及範圍、創造營收和啟動全域對象的複雜性。此外，Primetime 也提供了以下解決方案和值：

   * 支援準確測量線性和 VOD 內容類型。
   * 支援測量包含 (或不包含) 動態廣告插入的廣告插播。
   * TVSDK 的流暢廣告插入模型允許直接測量廣告播放的分析，進而提高準確性。
   * 強大的事件和中繼資料集合，可確保跨 QoS 緩衝或行動連線中斷問題以及一般使用者互動 (例如在行動裝置上搜尋、暫停和背景處理) 的準確性。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK 已與 Media Analtyics (心率) SDK 整合，使得在每個支援的平台上實作時更加簡單快速。<!--Primetime also supports the partnership with Nielsen.-->若要利用 Primetime，請遵循在以下內容中找到的相同指引和必要條件: [用戶端](/help/intro-to-ava/implementation-paths/client-side-path.md)以及適用於您平台的下列文件: [Primetime 使用手冊](https://helpx.adobe.com/tw/primetime/user-guide.html)。

您也應該聯絡銷售代表/客戶經理，討論購買 TVSDK 的所需作業。
