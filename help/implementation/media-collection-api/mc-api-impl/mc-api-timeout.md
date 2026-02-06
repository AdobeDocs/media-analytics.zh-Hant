---
title: 逾時條件
description: 瞭解Media Collection API逾時條件。
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 60%

---

# 逾時條件{#timeout-conditions}

**媒體收集 API 逾時條件**

媒體收集 API 是無狀態 API，不像 Media SDK 一樣具備在逾時條件發生時發行新工作階段 ID 的機制。發生逾時條件時，後端會關閉工作階段，並捨棄所有後續使用該工作階段ID進行的呼叫。 處理工作階段逾時的邏輯必須在使用者端中處理。 也就是說，播放器必須監控逾時條件，並在逾時發生時取得新的工作階段ID。

* **10 分鐘：沒有 API 事件**

  如果後端未接收到任何 API 事件，將會關閉工作階段。
* **30 分鐘：播放點未變更**

  如果播放點在 30 分鐘內未移動 (例如，使用者點擊「暫停」並離開座位)，後端將會關閉工作階段。

>[!NOTE]
>
>您也可以傳送 `sessionEnd` 事件類型的 `events` 要求來強制結束工作階段。
