---
title: 關於心率測量
description: 了解如何使用心率來收集視訊量度。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# 關於心率測量

Adobe Analytics使用「心率」來收集視訊量度。 視訊播放期間，系統會將心率傳送至心率追蹤伺服器，以測量播放時間。心率呼叫每十秒傳送一次。心率可產生精細的視訊參與量度，以及更精確的視訊流失報表。Adobe Analytics for Streaming Media使用Media Launch搭配Media Analytics擴充功能、Media SDK和Media Collection API來測量心率。 系統會使用 `AppMeasurement` 和 `VisitorID` 元件來接收視訊資料。

使用 Adobe Analytics for Streaming Media 的心率功能有以下優勢：

| 功能 | 說明 |
|---|---|
| 媒體事件 | 應用於主要內容時，詳細和自訂事件會每 10 秒傳送一次；若是應用於廣告，則每 1 秒傳送一次 |
| 度量和維度 | 清楚的標準化量度、維度和跨廠商的基準。透過跨所有平台的標準化解決方案，您可以在所有媒體和平台上使用一致的標準化變數，以進行更有效率的跨促銷活動、裝置和廠商比較。 |
| 整合 | Experience CloudID會連結至Adobe Experience Cloud，以便進行交叉分析。透過自動Adobe Experience Cloud整合，您可以劃分媒體對象、鎖定這些對象，並根據使用者偏好提出媒體建議。 |
| 定價 | 依據媒體資料流 (單次) 進行透明化追蹤 |
| 實作與支援 | 透過持續更新和改善來簡化設定。透過簡化的實作程式，您可以透過播放器API快速對應變數，並使用Adobe除錯工具來驗證實作，以確保所有必要變數皆受到精確追蹤。 |
| 合作夥伴共用 | Federated Analytics和認證量度。透過Federated Analytics的共用資料，您可以利用我們領先業界的媒體共用功能，跨越所有媒體經銷商合作夥伴（操作員、程式設計人員和經銷商）全面評估資料。 |
| 進階追蹤 | 下載內容追蹤、錯誤修復追蹤和同時觀看者。您可以追蹤下載到裝置上播放的串流媒體內容（不論是否連上網路）。 |
