---
title: 播放器狀態追蹤範例
description: 此主題舉例說明「播放器狀態追蹤」功能。
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 100%

---


# 播放器狀態追蹤範例


## 長暫停範例

當視訊工作階段的暫停持續時間超過 30 分鐘時，API 需要新的工作階段。發生此情況時，用戶端必須產生新的工作階段 ID。  對於這兩個視訊工作階段，用戶端應保留播放器所處的所有狀態，並在 `sessionStart` 呼叫後立即將所有資訊當成 `stateStart` 事件傳送。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

傳送 `sessionEnd` 後，必須開始新的視訊工作階段，第一個 API 事件為：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長暫停範例顯示播放器也會儲存其狀態，以便傳送給新視訊工作階段。
