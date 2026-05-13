---
title: 逾時條件
description: 瞭解Media Collection API逾時條件。
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# 逾時條件{#timeout-conditions}

**媒體收集 API 逾時條件**

媒體收集 API 是無狀態 API，不像 Media SDK 一樣具備在逾時條件發生時發行新工作階段 ID 的機制。 發生逾時條件時，後端會關閉工作階段，並捨棄所有後續使用該工作階段ID進行的呼叫。 處理工作階段逾時的邏輯必須在使用者端中處理。 也就是說，播放器必須監控逾時條件，並在逾時發生時取得新的工作階段ID。

* **10 分鐘：沒有 API 事件**

  如果後端未接收到任何 API 事件，將會關閉工作階段。
* **30 分鐘：播放點未變更**

  如果播放點在 30 分鐘內未移動 (例如，使用者點擊「暫停」並離開座位)，後端將會關閉工作階段。

>[!NOTE]
>
>您也可以傳送 `sessionEnd` 事件類型的 `events` 要求來強制結束工作階段。
