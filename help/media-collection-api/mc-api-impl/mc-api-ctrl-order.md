---
title: 控制事件順序
description: 控制事件順序
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: e0da35f364dc057a241fbb05a718a731ffee1e94
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# 控制事件順序{#controlling-the-order-of-events}

串流視訊追蹤是高度依時間而定的作業，有時候Media Collection API追蹤呼叫會在後端逾時到達。 在這種情況下，後端會嘗試根據`playerTime`物件中提供的時間戳記，將事件排入佇列並重新排序。  發生此情況時有一些限制。 目前，如果失序呼叫之間的延遲超過一秒，則重新排序可能會失敗。 在未來的更新中，「可接受的延遲時間」可能會最佳化並加以設定。

## 無序事件範例
當事件通過網路時發生順序錯誤事件，這有時會導致延遲。

例如，您可以傳送`adBreakStart`事件，後面接著`adStart`事件。 這是常見的使用案例，因為廣告必須從廣告插播中開始。

如果廣告已就緒且不需要緩衝區，則兩個事件幾乎都會立即發生，且兩個事件的`playerTime.ts`彼此非常接近——但它們永遠不應相等。

> 事件的「playerTime.ts」對於任何事件都不應等於，因為排序演算法不會先知道發生了什麼事件。 每2個連續事件至少應有1毫秒的時間戳差。

由於兩個事件在觸發網路呼叫時都會及時發生，因此可能會發生故障。 在此範例中，`adStart`事件會在`adBreakStart`事件之前到達。


有一個事件的計時窗口：5秒或最多10個事件。 在將事件傳送至處理管線之前，會先緩衝這些事件。 當滿足條件時- 5秒已經過或接收10個以上事件時，會根據`playerTime.ts`重新排序事件，然後以新順序傳送至處理管道。

>[!IMPORTANT]
>
>有個例外事件會立即發送到處理流水線，即`sessionStart`事件。
