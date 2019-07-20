---
seo-title: 逾時條件
title: 逾時條件
uuid: 2a4ea13e-a561-4adf-b567-f980301 b32 c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 逾時條件{#timeout-conditions}

**Media Collection API逾時條件**

媒體收集API(無狀態)與Media SDK無相同機制，可在逾時條件發生時發出新的階段作業ID。當逾時條件發生時，後端會關閉工作階段，因此所有以該工作階段 ID 發出的後續呼叫都將遭到捨棄。處理工作階段逾時的邏輯必須在用戶端中處理。也就是說，播放器必須監控逾時條件，並在逾時發生時取得新的工作階段 ID。

* **10分鐘：無API事件**

   如果後端未收到任何API事件，則會關閉工作階段。
* **30分鐘：無播放磁頭變更**

   如果播放磁頭未移動30分鐘(例如，使用者點擊暫停並離開)，後端會關閉工作階段。

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

