---
title: 控制事件順序
description: 了解如何控制事件的順序，以及在某些情況下如何根據playerTime物件中提供的時間戳記重新排序事件。
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# 控制事件順序{#controlling-the-order-of-events}

串流視訊追蹤是一項高度依賴時間的作業，有時媒體收集API追蹤呼叫會未依順序進入後端。 在此情況下，後端會根據`playerTime`物件中提供的時間戳記，嘗試將事件加入佇列及重新排序。  這會有一些限制。 目前，如果順序錯誤呼叫之間的延遲超過一秒，則重新排序可能會失敗。 在未來的更新中，「可接受的延遲時間」可以優化和配置。

## 順序錯誤事件範例

事件通過網路時發生順序錯亂的事件，這有時會導致延遲。

例如，您可以傳送`adBreakStart`事件，後接`adStart`事件。 這是常見的使用案例，因為廣告是從廣告插播開始的必要動作。

如果廣告就緒且不需要緩衝，兩個事件幾乎都會立即發生，且兩個事件的`playerTime.ts`非常接近，但絕不應相等。

> 事件的「playerTime.ts」在任何事件中都不應相等，因為排序演算法不會知道先發生了什麼事件。 每2個連續事件的時間戳記差異應至少為1毫秒。

因為兩個事件在觸發網路呼叫時都會非常接近，因此可能會不正常送達。 在此範例中， `adStart`事件在`adBreakStart`事件之前到達。


有一個事件計時視窗：5秒或最多10個事件。 在將事件傳送至處理管道之前，會先緩衝這些事件。 當符合條件時 — 已經過5秒或接收了10多個事件，則會根據`playerTime.ts`重新排序事件，然後以新順序發送到處理管道。

>[!IMPORTANT]
>
>有個例外事件會立即傳送至處理管道，即為`sessionStart`事件。
