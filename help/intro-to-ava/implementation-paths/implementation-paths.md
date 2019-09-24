---
seo-title: 實施路徑
title: 實施路徑
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 實施路徑 {#implementation-paths}

Media Analytics(Heartbeats)是Adobe的標準化視訊解決方案。 它已經取代 Adobe 的舊版里程碑模型。

對於這些實作路徑，客戶必須聯絡其銷售代表／客戶經理以簽署新的銷售訂單，因為Media Analytics有唯一的SKU，而且從根據伺服器呼叫的定價模型變更為以視訊串流為基礎的模型：

* **用戶端** -這些僅與媒體分析整合。 您可以選擇視訊心率 SDK 與/或媒體收集 API 整合。此路徑可用於任何視訊播放器，包括客戶及/或 OVP 播放器，例如 Brightcove、Ooyala、thePlatform 等。

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >若要使用媒體分析，客戶也必須使用Adobe Analytics。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch是動態標籤管理的後續產品，其功能是提供Media Analytics Launch Extension，可協助您在播放器中實作視訊追蹤。

   您可以透過以下網址進一步瞭解Experience Platform Launch:音訊 [與視訊擴充功能的Adobe Media Analytics](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** Adobe Primetime是Adobe Experience cloud解決方案，可協助內容節目編排者和發佈者透過每個連線螢幕的媒體獲利。

   Primetime 藉由提供模組化平台以進行視訊發佈、廣告刊登、個人化和分析，消除了各裝置之間的可及範圍、創造營收和啟動全域對象的複雜性。此外，Primetime 也提供了以下解決方案和值:

   * 支援準確測量線性和 VOD 內容類型。
   * 支援評量包含 (或不包含) 動態廣告插入的廣告插播。
   * TVSDK 的流暢廣告插入模型允許直接測量廣告播放的分析，進而提高準確性。
   * 強大的事件和中繼資料集合，可確保跨 QoS 緩衝或行動連線中斷問題以一般使用者互動 (例如在行動裝置上搜尋、暫停和後台處理) 的準確性。
   * Nielsen DTVR (線性) 與 ID3 中繼資料以及 DCR 與 CMS 中繼資料的整合支援。
   TVSDK is already integrated with the Media Analtyics (Heartbeats) SDK, which makes implementation much easier and faster across every supported platform. Primetime 也支援與 Nielsen 合作。若要利用 Primetime，請遵循在以下內容中找到的相同指引和必要條件: [用戶端](/help/intro-to-ava/implementation-paths/client-side-path.md)以及適用於您平台的下列文件: Primetime使 [用指南。](https://helpx.adobe.com/primetime/user-guide.html)

   您也應該聯絡銷售代表/客戶經理，討論購買 TVSDK 的所需作業。
