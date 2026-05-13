---
title: 關於心率測量
description: 了解如何使用心率收集視訊量度。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e6c28e30-8689-4bf4-8fa8-561343d308a9
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# 關於心率測量

Adobe串流媒體服務使用「心率」收集視訊量度。 視訊播放期間，系統會將心率傳送至心率追蹤伺服器，以測量播放時間。 心率呼叫每十秒傳送一次。 心率可產生精細的視訊參與量度，以及更精確的視訊流失報表。 串流媒體服務會使用Adobe Launch搭配Media Analytics擴充功能、Media SDK和媒體收集API來測量心率。 系統會使用 `AppMeasurement` 和 `VisitorID` 元件來接收視訊資料。

在串流媒體服務中使用心率有以下優勢：

| 功能 | 說明 |
|---|---|
| 媒體事件 | 應用於主要內容時，詳細和自訂事件會每 10 秒傳送一次；若是應用於廣告，則每 1 秒傳送一次 |
| 度量和維度 | 清楚的標準化量度、維度和不同廠商的效能評定。 透過跨所有平台的標準化解決方案，您可以在所有媒體和平台上使用一致的標準化變數，以提升比較不同促銷活動、裝置和廠商的效率。 |
| 整合 | Experience Cloud ID與Adobe Experience Cloud相互連結，使交叉分析更為輕鬆。 透過自動整合Adobe Experience Cloud，您可以劃分及鎖定媒體對象，並根據使用者偏好提出媒體建議。 |
| 定價 | 依據媒體資料流 (單次) 進行透明化追蹤 |
| 實作與支援 | 透過持續更新和改進簡化設定。 透過簡化的實作程式，您可以透過播放器API快速對應變數，並使用Adobe Debug Tool驗證實作，以確保所有必要變數皆受到精確追蹤。 |
| 合作夥伴共用 | 同盟媒體和認證量度。 透過Federated Media的共用資料，您可以利用我們領先業界的媒體共用功能，跨越所有媒體經銷商合作夥伴（業者、程式設計人員和經銷商）全面評估資料。 |
| 進階追蹤 | 下載內容追蹤、錯誤修復追蹤和同時觀看者。 您可以追蹤下載到裝置上播放的串流媒體內容（不論是否連上網路）。 |
