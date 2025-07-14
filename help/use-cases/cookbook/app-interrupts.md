---
title: 在播放期間處理應用程式中斷狀況
description: 了解如何處理媒體播放期間追蹤中斷的問題。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 90%

---

# 在播放期間處理應用程式中斷狀況{#handling-application-interrupts-during-playback}

媒體應用程式中的播放作業可以透過多種方式中斷。例如，使用者可以明確地按下暫停，或者使用者可以將應用程式置於背景。不論導致媒體播放中斷的原因為何，追蹤指示保持不變。

1. 當應用程式中斷 (進入背景、媒體暫停等) 時，呼叫 **`trackPause`**。
1. 當應用程式返回前景及/或媒體恢復播放時，呼叫 **`trackPlay`**。

>[!NOTE]
>
>當應用程式從背景返回時呼叫`trackSessionStart`，可能會導致截至該時間點為止的播放未計入播放時間總計，而且也會遺失先前的進度標籤、區段等。 反之，當應用程式返回及/或媒體恢復播放時，請呼叫 `trackPlay`。

## 有關如何處理應用程式中斷的常見問題集： {#faq-about-handling-application-interrupts}

* _應用程式要在背景停留多長的時間後，才應關閉工作階段?_

  如果應用程式允許背景播放，它能呼叫我們的 API 來繼續追蹤，我們也會照常傳送所有追蹤 Ping。除了 YouTube Red 之外，並沒有很多視訊應用程式允許背景播放，但所有音訊應用程式皆允許這項功能。如果應用程式不允許背景播放，建議您在此暫停狀態維持一分鐘後再結束追蹤工作階段。應用程式無法繼續傳送暫停 Ping，因為在大部分情況下，它無法判斷使用者是否會回來繼續觀看媒體，也無法判斷應用程式何時會終止。如果應用程式停留在背景時繼續傳送 Ping，也會帶來不良的體驗。

* _應用程式長時間停留在背景之後，要怎麼處理重新啟動追蹤才是正確的做法?_

  應用程式應呼叫 `trackSessionEnd` 來結束追蹤工作階段。從 2.1 版開始，SDK 會傳送「結束」Ping 來通知後端追蹤工作階段已關閉。

* _要如何重新啟動同一個工作階段?_

  如需有關恢復追蹤工作階段的資訊，請參閱[恢復非作用中工作階段](resuming-inactive.md)。SDK 會傳送恢復 Ping 以通知後端使用者正手動恢復工作階段。
