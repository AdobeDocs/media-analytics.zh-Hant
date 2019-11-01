---
title: 逾時條件
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 逾時條件{#timeout-conditions}

**Media Collection API逾時條件**

Media Collection API為無狀態，與Media SDK沒有相同的機制，無法在逾時條件發生時發出新的工作階段ID。 當逾時條件發生時，後端會關閉工作階段，因此所有以該工作階段 ID 發出的後續呼叫都將遭到捨棄。處理工作階段逾時的邏輯必須在用戶端中處理。也就是說，播放器必須監控逾時條件，並在逾時發生時取得新的工作階段 ID。

* **10分鐘：無API事件**

   如果後端未收到任何API事件，則會關閉工作階段。
* **30分鐘：無播放頭變更**

   如果播放頭30分鐘內未移動（例如，使用者點擊「暫停」並走開），則後端會關閉作業。

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

