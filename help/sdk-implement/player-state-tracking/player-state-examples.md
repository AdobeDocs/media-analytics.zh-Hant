---
title: 播放器狀態追蹤範例
description: 本主題包含播放器狀態追蹤功能的範例。
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# 播放器狀態追蹤範例


## 長暫停範例

當視訊工作階段的暫停持續時間超過30分鐘時，API需要新的工作階段。 發生此情況時，客戶端應生成新的會話ID。 對於這兩個視訊作業，用戶端應保留播放器所處的所有狀態，並在呼叫後立即將所有資訊 `stateStart` 當成事件 `sessionStart` 傳送。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

傳送 `sessionEnd` 後，必須啟動新的視訊工作階段，第一個API事件為：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長暫停範例顯示播放器也儲存其狀態，以便傳送至新視訊作業。
