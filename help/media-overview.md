---
seo-title: 在 Adobe Analytics 測量音訊和視訊
title: 在 Adobe Analytics 測量音訊和視訊
uuid: b3cbe240-b94 d-42b8-a99 c-0280334aa14
translation-type: tm+mt
source-git-commit: 1915261ec21679f510350663a472096abe7fdf63

---


# 在 Adobe Analytics 測量音訊和視訊{#measuring-audio-and-video-in-adobe-analytics}

![橫幅](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. 它不包含舊有里程碑視訊實施的相關指示。我們鼓勵所有客戶儘量採用這兩個最新的媒體追蹤解決方案其中之一或兩項，以便充分利用其改進項目和擴充的測量功能。您可以查看下列[轉換為最新解決方案的優點](media-overview.md#section_cnj_5st_p1b)。雖然我們將繼續支援里程碑方法，但不會有任何計劃更新、修正或功能改進。如有任何問題，請洽詢您的 Adobe 客戶經理。

## 概述 {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media (亦稱為 Media Analytics) 為基本 Analytics 產品的附加元件，提供客戶強大的內容、音訊和廣告媒體測量。Media Analytics 提供客戶即時監控、詳細分析、可行的洞察和營利商機等多項優勢。

媒體追蹤是透過下列任一項作業啟動:

* **Media SDK -** 整合最常使用的媒體播放器。
* **媒體收集 API -** (RESTful API) 整合無 SDK 支援的播放器 (或不想整合 SDK 的播放器)。

   媒體收集 API 也具備 SDK 中未具備的其他功能。

   * **追蹤下載內容 -** 支援追蹤下載並在裝置播放 (不論是否有連線) 的媒體內容 (視訊與音訊)。此功能以媒體收集 API 為基礎來打造，採用相同的播放器追蹤規格。(目前不支援 SDK。)

Adobe Analytics for Media 讓用戶端可以追蹤客戶在其網站上的完整歷程 (包括媒體使用情況)，而且這些測量功能可輕鬆整合在 Analytics 報表和其他 Experience Cloud 產品中。媒體測量可讓您將資料劃分至多個維度和區段，擷取您要進行完整詳細分析所需的所有中繼資料，並將成功條件歸為完整使用的內容、平均逗留時間以及結束的廣告。

媒體解決方案不只測量與 QoS 相關的重要傳送量度，如中斷、緩衝逗留時間和平均位元速率。亦可結合網站或應用程式資料，將客戶和客戶興趣流程視覺化，更能提出建議，並透過 Adobe Experience Cloud 客製化客戶體驗。

## 福利 {#section_7712BA90EAE64C118218D1C581EF68B7}

Adobe 的媒體測量解決方案提供的部分優勢包括:

* **及時分析 -** 使用跨越多個管道的關鍵效能量度 (例如持續時間) 來做出即時且可行的決定。主要內容事件是以 **10 秒鐘**&#x200B;的間隔來測量，以擷取其發生所有活動。廣告追蹤事件則為 **1 秒鐘**&#x200B;的發生間隔。
* **促進參與 -** 透過較少的緩衝事件和瞭解廣告播放在內容中的時間和位置，提供較少干擾的流暢體驗，讓使用者回頭重複造訪，進而與使用者全面互動。
* **全面性的圖片-** 結合所有內容發佈者的多個資料點，以獲得所有媒體活動的完整檢視，並透過 [Federated Analytics](federated-analytics.md) 功能衡量所有可能通道的參與與檢視/偵聽/偵聽。
* **提高粒度 -** 從最精細的層級評估檢視行為，包括個別訪客的每日時間、每分鐘的同時檢閱者/聽眾人數以及使用內容的平均持續時間。
* **精準的測量 -** 跨越用來使用媒體的多項裝置進行測量，包括 OTT、智慧型手機、平板電腦、桌面等，以監控使用者的參與類型和習慣。
* **區段 -** 套用分類至您的播放器、裝置、類型、章節，並顯示每一個類別如何影響整體的檢視/收聽次數，以及客戶對內容、音訊、廣告和複合上述項目的參與度。

## 心率優點對比里程碑優點 {#section_cnj_5st_p1b}

Adobe Analytics for Media可透過兩種方式進行測量：舊版里程碑方法(僅限視訊)和目前的心率方法(音訊和視訊，包括Media SDK和Media Collection API)。我們建議使用「心率」方法進行測量，也鼓勵所有用戶端改用此版本 (如果還沒改用的話)，以充分利用下述的各項優點。

舊版的「里程碑」方法是根據個別伺服器對 Analytics 伺服器的呼叫，可適用於影片開始、四分位數、持續期間和完成。「心率」方法提供更為強大的媒體追蹤解決方案，以 10 秒鐘間隔測量主要內容，提供強化的標準量度。此外，Adobe 從「里程碑」淬鍊出更為進步的功能，可透過心率使用的 Media SDK 或媒體收集 API 提供較為流暢的簡化實作程序。

在此羅列「心率」方法的幾項優點:

* **簡化實作程序 -** 透過播放器 API 對應變數更為輕鬆，並可透過 Adobe Debug 工具來驗證實作，確保所有必要的變數均已準確追蹤。
* **Adobe Experience Cloud 自動整合** - 透過 Experience Cloud ID 與 Adobe Experience Cloud 自動整合、劃分和鎖定媒體受眾、以及根據使用者偏好提出媒體建議。
* **透過同盟分析共用資訊 -** 利用我們業界領先的媒體共用功能，跨越所有媒體經銷商合作夥伴 (操作員、程式設計人員和經銷商) 全面評估資料。
* **與獲得認證的收視率合作夥伴合作 -** Adobe 與觀眾收視率合作夥伴 Nielsen 合作提供中立的人口統計第三方測量，推出值得信賴的認證收視率。
* **跨所有平台的標準化解決方案 -** 啟用跨越所有媒體和平台一致的標準化變數，以進行更有效率的跨促銷活動、裝置和廠商的比較。

### 比較表

|  | Video Analytics - 里程碑 | Media Analytics - 心率 |
|---|---|---|
| **媒體事件** | 高階標準事件 | 主要內容每 10 秒鐘測量一次詳細的自訂事件，廣告則每 1 秒鐘測量一次 |
| **度量和維度** | 廠商之間的差異、非標準化量度和維度 | 清楚的標準化量度、維度和不同廠商的效能評定 |
| **與 Adobe 產品的整合** | 包含配對和整合的個別工作階段 | 連結至完整 Adobe Experience Cloud 以及輕鬆進行交叉分析之已結合的 Experience Cloud ID |
| **定價** | 針對每個伺服器呼叫進行追蹤和計費 | 透過媒體資料流 (單次) 進行透明化的追蹤 |
| **實作與支援** | 與舊版延長整合，提供有限的支援，但不再進行更新 | 包含持續更新和改良之簡化設定 |
| **合作夥伴共用** | 不適用 | 同盟分析與經認證的量度 |
| **進階追蹤** | 不適用 | 錯誤修復追蹤和同時觀看者 |

## 支援的裝置 {#section_lkm_l5t_p1b}

Adobe Analytics for Media 隨業界發展與時俱進，提供強大的資料收集工具，以確保在所有重要的裝置，對每一個媒體資料流進行收集和報表。我們開發的 Media SDK 可適用於所有最多人使用的裝置，包括:

* iOS 和 Android 智慧型手機和平板電腦
* 適用於 ROKU、AppleTV、FireTV 以及 Android TV 的 OTT 裝置
* 適用於桌上型電腦和筆記型電腦的 JavaScript 瀏覽器

裝置發佈新版本時，SDK 會定時更新，供您將這些 SDK 用來與目前大多數的大型媒體播放器整合，包括 Brightcove 和 Ooyala。

針對目前無 SDK 支援的裝置或平台 (或者即使有)，您可以執行媒體收集 API，藉此直接從裝置/平台對 Media Analytics 後端進行 RESTful API 呼叫。

下列表格提供目前透過我們的 Media SDK 實作和媒體收集 API 實作支援的裝置清單。若要下載最新版 SDK，請參閱[下載 SDK。](sdk-implement/download-sdks.md)如果您要搜尋測量的裝置並未列入上述清單中，請聯絡客戶服務或您的解決方案顧問，諮詢該裝置的狀態。

|      | Media SDK | 媒體收集 API |
|---|:---:|:---:|
| **JavaScript 瀏覽器** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS 裝置** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android 裝置** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **統一的 Windows 平台 (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (新版/舊版)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (原生應用程式)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(其他/新連接裝置)** |  | ![](assets/icon-blue-check.png) |

For Media SDK, also see [Minimum Platform Version Support](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS注意事項—** Adobe的安全性規範標準需要舊版安全性通訊協定的結束生命週期。為了持續符合不斷發展的安全性通訊協定標準，Adobe正致力於使用TLS1.2，以提供最新和最安全的版本。自2019年月20日起，Adobe僅支援TLS1.1或更新版本。在此項變更後，Adobe將不再透過部署TLS1.0的舊裝置或網頁瀏覽器收集使用者資料。移轉至TLS1.2可改善安全性。務必詳閱詳細資訊，並針對變更進行規劃，以順利轉移。

>[!NOTE]
>
>TLS目前已部署在網頁瀏覽器和其他要求安全交換網路的應用程式中，目前已採用最廣泛部署的安全性通訊協定。
