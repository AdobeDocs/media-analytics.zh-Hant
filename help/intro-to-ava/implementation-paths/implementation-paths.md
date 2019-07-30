---
seo-title: 實施路徑
title: 實施路徑
uuid: 8400c938-e77 e-4c88-b23 b-5f5977 a5316 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 實施路徑 {#implementation-paths}

媒體分析(Heartbeats)是Adobe的標準化視訊解決方案。它已經取代 Adobe 的舊版里程碑模型。

對於上述每個實施路徑，客戶必須聯絡其銷售代表/客戶經理以簽署新的銷售訂單，因為媒體Analytics有一個唯一SKU和從根據伺服器呼叫的模型呼叫變更為基於視訊串流的模型：

* **用戶端-** 這些是僅限Media Analytics的整合。您可以選擇視訊心率 SDK 與/或媒體收集 API 整合。此路徑可用於任何視訊播放器，包括客戶及/或 OVP 播放器，例如 Brightcove、Ooyala、thePlatform 等。

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >若要使用Media Analytics，客戶也必須使用Adobe Analytics。

* **Adobe Experience Platform Launch-** Adobe Experience Platform Launch是Dynamic Tag Management的後續產品，提供Media Analytics Launch Extension，可協助您在播放器中實施視訊追蹤。

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime-** Adobe Primetime是Adobe Experience Cloud解決方案，可幫助內容節目編排者和發佈商在每個互聯螢幕上賺取媒體收入。

   Primetime 藉由提供模組化平台以進行視訊發佈、廣告刊登、個人化和分析，消除了各裝置之間的可及範圍、創造營收和啟動全域對象的複雜性。此外，Primetime 也提供了以下解決方案和值:

   * 支援準確測量線性和 VOD 內容類型。
   * 支援評量包含 (或不包含) 動態廣告插入的廣告插播。
   * TVSDK 的流暢廣告插入模型允許直接測量廣告播放的分析，進而提高準確性。
   * 強大的事件和中繼資料集合，可確保跨 QoS 緩衝或行動連線中斷問題以一般使用者互動 (例如在行動裝置上搜尋、暫停和後台處理) 的準確性。
   * Nielsen DTVR (線性) 與 ID3 中繼資料以及 DCR 與 CMS 中繼資料的整合支援。
   TVSDK已與Media Publishics(Heartbeats) SDK整合，讓每個支援的平台更輕鬆快速地實施。Primetime 也支援與 Nielsen 合作。若要利用 Primetime，請遵循在以下內容中找到的相同指引和必要條件: [用戶端](/help/intro-to-ava/implementation-paths/client-side-path.md)以及適用於您平台的下列文件:[Primetime使用指南。](https://helpx.adobe.com/primetime/user-guide.html)

   您也應該聯絡銷售代表/客戶經理，討論購買 TVSDK 的所需作業。
