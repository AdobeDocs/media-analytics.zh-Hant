---
title: 控制事件順序
description: 了解如何控制事件順序，以及在某些情況下如何根據 playerTime 物件中提供的時間戳記將事件重新排序。
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# 控制事件順序{#controlling-the-order-of-events}

串流視訊追蹤是高度依賴時間的操作，有時 Media Collection API 追蹤呼叫未依照順序到達後端。在此情況下，後端會嘗試根據 `playerTime` 物件中提供的時間戳記，將事件加入佇列及重新排序。此操作有一些限制。目前，如果順序錯亂之呼叫間的延遲時間超過一秒，重新排序就可能會失敗。在未來的更新中，「可接受的延遲時間」可能會最佳化和可設定。

## 順序錯亂事件範例

當事件通過的網路有時會導致延遲時，就會發生順序錯亂事件。

例如，您可以傳送一個 `adBreakStart` 事件，然後傳送一個 `adStart` 事件。這是一個常見的使用案例，因為在廣告插播中需要開始廣告。

如果廣告準備就緒且無需緩衝，則兩個事件幾乎立即發生，且兩個事件的 `playerTime.ts` 彼此非常接近 - 但它們絕不應該相等。

> 事件的「playerTime.ts」絕不應該與任何事件相等，因為排序演算法不知道哪個事件先發生。每 2 個連續事件的時間戳記應該相差至少 1 毫秒。

因為這兩個事件在觸發網路呼叫時彼此發生的時間非常接近，所以它們可能會未依順序到達。在此範例中，`adStart` 事件在 `adBreakStart` 事件之前到達。


事件會有一個定時時段：5 秒或最多 10 個事件。事件在傳送到處理管道之前會被緩衝。當滿足條件時 - 經過 5 秒或收到超過 10 個事件，事件將根據 `playerTime.ts` 重新排序，然後以新順序傳送到處理管道。

>[!IMPORTANT]
>
>有一個例外事件會立即傳送到處理管道，即 `sessionStart` 事件。
