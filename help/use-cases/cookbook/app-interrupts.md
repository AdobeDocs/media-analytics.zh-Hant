---
title: 在播放期間處理應用程式中斷狀況
description: 了解如何處理媒體播放期間追蹤中斷的問題。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 63%

---

# 在播放期間處理應用程式中斷狀況{#handling-application-interrupts-during-playback}

媒體應用程式中的播放作業可以透過多種方式中斷。例如，使用者可以明確地按下暫停，或者使用者可以將應用程式置於背景。不論導致媒體播放中斷的原因為何，追蹤指示保持不變。

1. 當應用程式中斷 (進入背景、媒體暫停等) 時，呼叫 **`trackPause`**。
1. 當應用程式返回前景及/或媒體恢復播放時，呼叫 **`trackPlay`**。

>[!NOTE]
>
>當應用程式從背景返回時呼叫`trackSessionStart`，可能會導致截至該時間點為止的播放未計入播放時間總計，而且也會遺失先前的進度標籤、區段等。 反之，當應用程式返回及/或媒體恢復播放時，請呼叫 `trackPlay`。

## 有關如何處理應用程式中斷的常見問題集： {#faq-about-handling-application-interrupts}

* _應用程式應在工作階段關閉前多久進入背景執行？_

  如果應用程式允許背景播放，則可藉由呼叫我們的API繼續追蹤，而我們將傳送所有定期追蹤Ping。 除了 YouTube Red 之外，並沒有很多視訊應用程式允許背景播放，但所有音訊應用程式皆允許這項功能。如果應用程式不允許背景播放，建議您在此暫停狀態維持一分鐘後再結束追蹤工作階段。應用程式無法繼續傳送暫停 Ping，因為在大部分情況下，它無法判斷使用者是否會回來繼續觀看媒體，也無法判斷應用程式何時會終止。在背景持續傳送Ping也是不好的體驗。

* _應用程式在背景執行很長時間後，處理重新啟動追蹤的正確方式為何？_

  應用程式應呼叫 `trackSessionEnd` 來結束追蹤工作階段。從2.1版開始，SDK會傳送「結束」Ping以通知後端追蹤工作階段已關閉。

* _重新啟動相同工作階段怎麼樣？_

  如需有關恢復追蹤工作階段的資訊，請參閱[恢復非作用中工作階段](resuming-inactive.md)。SDK 會傳送恢復 Ping 以通知後端使用者正手動恢復工作階段。
