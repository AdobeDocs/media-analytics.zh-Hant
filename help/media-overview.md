---
title: 在 Adobe Analytics 測量音訊和視訊
description: Adobe Analytics for Media (亦稱為 Media Analytics) 可提供客戶強大的內容、音訊和廣告媒體測量。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# 在 Adobe Analytics 測量音訊和視訊{#measuring-audio-and-video-in-adobe-analytics}

![橫幅](./assets/media_analytics_banner.png)

## 關於Adobe Analytics for Audio and Video

Adobe Analytics for Audio and Video是Adobe Analytics的附加元件，可為音訊、視訊和廣告提供強大的測量工具。 Adobe Analytics是Adobe Experience Platform的一部分。

Adobe Analytics for Audio and Video可讓您追蹤整個網站的客戶歷程。 這些量度可輕鬆整合至Adobe Analytics報表和其他Adobe Experience Cloud產品。 媒體測量可讓您將資料分為多個維度和區段，以擷取完成詳細分析所需的所有中繼資料。 然後，您可以分析資料並將成功標準歸因於完全使用的媒體、平均逗留時間和完成的廣告。

您可以測量與QoS相關的重要傳送量度，例如丟棄的影格、逗留時間緩衝和平均位元速率。 此外，這些指標可與您的網站或應用程式資料結合，以視覺化客戶路徑和興趣——使用Adobe Experience Cloud提供增強的建議並個人化客戶體驗。

## 功能 {#features}

Adobe Analytics的音訊和視訊優點包括即時監控、詳細分析、可操作見解和獲利機會。
* **即時分析**—跨多個通道利用關鍵效能量度（例如持續時間、ex2和ex3）進行即時、可操作的決策。 主要內容事件是以 10 秒鐘的間隔來測量，以擷取其發生所有活動。廣告追蹤事件則為 1 秒鐘的發生間隔。
* **推動參與**—透過減少緩衝事件，並瞭解廣告在內容中的播放位置和播放時間，提供順暢、不受干擾的體驗，以提供重複瀏覽，進而與使用者充分互動。
* **全貌**—將多個資料點整合到所有內容發佈商，以全面瞭解您的所有媒體活動。 透過Federated Analytics功能，跨所有可能的通道測量參與和檢視／監聽。
* **增加詳細程度**—評估最細微的檢視行為，包括每日個別訪客時間、按分鐘的並行檢視器／監聽器，以及使用內容的平均持續時間。
* **精確度量**—測量用於媒體消費的多種裝置，包括OTT、智慧型手機、平板電腦、案頭等，以監控使用者參與模式和習慣。
* **細分**—將分類套用至您的播放器、裝置、類別、章節，並顯示每個分類對您的整體檢視／監聽和客戶參與（包括內容、音訊、廣告和組合）的影響。

## 心率測量 {#heartbeat}

Adobe Analytics使用「心率」來收集視訊量度。 在視訊播放期間，心率會傳送至心率追蹤伺服器，以測量播放時間。 心跳呼叫每十秒傳送一次。 心率可產生精細的視訊參與度量，並產生更精確的視訊流失報表。 Adobe Analytics for Audio and Video使用Adobe Launch搭配Media Analytics擴充功能、Media SDK和Media Collection API測量心率。 該 `AppMeasurement` 和 `VisitorID` 元件用來接收視訊資料。

使用Adobe Analytics的音訊和視訊心率可提供下列優點：

| 功能 | 說明 |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 媒體事件 | 詳細和自訂事件會每10秒傳送一次，用於主要內容，用於廣告則每1秒傳送一次 |
| 度量和維度 | 清晰的標準化指標、維度和基準<br>透過跨所有平台的標準化解決方案，您可以跨所有媒體和平台使用一致的標準化變數，以便更有效率地進行跨宣傳、裝置和廠商的比較。 |
| 整合 | Experience Cloud ID已連結至Adobe Experience Cloud，以便更輕鬆地進行交叉分析有了Adobe Experience Cloud自動整合，您可以細分媒體受眾、鎖定受眾，並根據用戶偏好提出媒體建議。<br> |
| 定價 | 透過媒體資料流 (單次) 進行透明化的追蹤 |
| 實作與支援 | 使用持續更新和改進來簡化<br>設定透過簡化的實作程式，您可以透過播放器API快速對應變數，並使用Adobe Debug Tool驗證實作，以確保精確追蹤所有必要的變數。 |
| 合作夥伴共用 | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| 進階追蹤 | 下載的內容追蹤、錯誤復原追蹤和並行檢視器<br>您可追蹤在裝置上下載和播放的音訊和視訊內容，不論其連線性為何。 |



## 安全性 {#security}

在Adobe，我們非常重視您數位資產的安全性。 從我們將安全性嚴格整合至內部軟體開發流程和工具到跨功能事件回應團隊，我們致力於主動且靈活。 此外，我們與合作夥伴、研究人員和其他產業組織的合作有助於我們瞭解最新的威脅與安全性最佳實務，並持續將安全性建置於我們提供的產品與服務中。


### 傳輸層安全性 {#transport-layer-security}

**TLS 通知 --** Adobe 設立安全性法規遵循標準，會要求終止使用舊版安全性通訊協定。為持續符合不斷改變的安全性通訊協定標準，Adobe 正在移轉為使用 TLS 1.2，以擁有最新且安全的使用中版本。自 2019 年 2 月 20 日起，Adobe 僅支援 TLS 1.1 或更新版本。經過這項變更後，Adobe 將不再從使用較舊裝置或部署 TLS 1.0 之網頁瀏覽器的使用者收集資料。移轉至 TLS 1.2 可提升安全性。務必詳閱詳細資訊，並針對變更進行規劃，以順利轉移。

>[!NOTE]
>
>TLS 是目前在須透過網路安全交換資料的網頁瀏覽器和其他應用程式中，最廣為部署的安全性通訊協定。
