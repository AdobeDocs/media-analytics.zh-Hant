---
title: 關於心率測量
description: 了解如何使用心率收集視訊量度。
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 75%

---

# 關於心率測量

Adobe串流媒體收集使用「心率」收集視訊量度。 視訊播放期間，系統會將心率傳送至心率追蹤伺服器，以測量播放時間。心率呼叫每十秒傳送一次。心率可產生精細的視訊參與量度，以及更精確的視訊流失報表。串流媒體會使用Adobe Launch搭配Media Analytics擴充功能、Media SDK和Media Collection API來測量心率。 系統會使用 `AppMeasurement` 和 `VisitorID` 元件來接收視訊資料。

在串流媒體收集中使用心率可提供下列優點：

| 功能 | 說明 |
|---|---|
| 媒體事件 | 應用於主要內容時，詳細和自訂事件會每 10 秒傳送一次；若是應用於廣告，則每 1 秒傳送一次 |
| 度量和維度 | 跨廠商的清晰標準化量度、維度和基準。透過跨所有平台的標準化解決方案，您可以在所有媒體和平台上使用一致的標準化變數，以提升比較不同促銷活動、裝置和廠商的效率。 |
| 整合 | Experience Cloud ID 與 Adobe Experience Cloud 相互連結，使交叉分析更為輕鬆。透過 Adobe Experience Cloud 自動整合，您可以劃分及鎖定媒體客群，並根據使用者偏好提出媒體建議。 |
| 定價 | 依據媒體資料流 (單次) 進行透明化追蹤 |
| 實作與支援 | 透過持續更新和改進來簡化設定。透過簡化的實作程序，您可以透過播放器 API 快速對應變數，並使用 Adobe Debug Tool 驗證實作，以確保所有必要變數皆受到精確追蹤。 |
| 合作夥伴共用 | 同盟媒體和認證量度。 透過Federated Media的共用資料，您可以利用我們領先業界的媒體共用功能，跨越所有媒體經銷商合作夥伴（業者、程式設計人員和經銷商）全面評估資料。 |
| 進階追蹤 | 下載內容追蹤、錯誤修復追蹤和同時觀看者。您可追蹤下載到裝置上播放的串流媒體內容 (不論是否連上網路)。 |
