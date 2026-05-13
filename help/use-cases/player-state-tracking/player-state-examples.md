---
title: 播放器狀態追蹤範例
description: 此主題舉例說明「播放器狀態追蹤」功能。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# 播放器狀態追蹤範例


## 長暫停範例

當視訊工作階段的暫停持續時間超過 30 分鐘時，API 需要新的工作階段。 發生此情況時，用戶端必須產生新的工作階段 ID。 對於這兩個視訊工作階段，用戶端應保留播放器所處的所有狀態，並在 `sessionStart` 呼叫後立即將所有資訊當成 `stateStart` 事件傳送。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

傳送 `sessionEnd` 後，必須開始新的視訊工作階段，第一個 API 事件為：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長暫停範例顯示播放器也會儲存其狀態，以便傳送給新視訊工作階段。
