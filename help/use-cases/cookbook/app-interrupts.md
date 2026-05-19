---
title: 在播放期間處理應用程式中斷狀況
description: 了解如何處理媒體播放期間追蹤中斷的問題。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 41%

---

# 在播放期間處理應用程式中斷狀況{#handling-application-interrupts-during-playback}

媒體應用程式中的播放作業可以透過多種方式中斷。 例如，使用者可以明確地按下暫停，或者使用者可以將應用程式置於背景。 不論導致媒體播放中斷的原因為何，追蹤指示保持不變。

1. 當應用程式中斷 (進入背景、媒體暫停等) 時，呼叫 **`trackPause`**。
1. 當應用程式返回前景及/或媒體恢復播放時，呼叫 **`trackPlay`**。

>[!NOTE]
>
>當應用程式從背景返回時呼叫`trackSessionStart`，可能會導致截至該時間點為止的播放未計入播放時間總計，而且也會遺失先前的進度標籤、區段等。 反之，當應用程式返回及/或媒體恢復播放時，請呼叫 `trackPlay`。

## 有關如何處理應用程式中斷的常見問題集： {#faq-about-handling-application-interrupts}

* _應用程式應在工作階段關閉前多久進入背景執行？_

  如果應用程式允許背景播放，則可藉由呼叫我們的API繼續追蹤，而我們將傳送所有定期追蹤Ping。 除了 YouTube Red 之外，並沒有很多視訊應用程式允許背景播放，但所有音訊應用程式皆允許這項功能。 如果應用程式不允許背景播放，建議您在此暫停狀態維持一分鐘後再結束追蹤工作階段。 應用程式無法繼續傳送暫停 Ping，因為在大部分情況下，它無法判斷使用者是否會回來繼續觀看媒體，也無法判斷應用程式何時會終止。 在背景持續傳送Ping也是不好的體驗。

* _應用程式在背景執行很長時間後，處理重新啟動追蹤的正確方式為何？_

  應用程式應呼叫 `trackSessionEnd` 來結束追蹤工作階段。 從2.1版開始，SDK會傳送「結束」Ping以通知後端追蹤工作階段已關閉。

* _重新啟動相同工作階段怎麼樣？_

  如需有關繼續追蹤工作階段的資訊，請參閱[繼續非作用中工作階段](resuming-inactive.md)。SDK會傳送恢復Ping來通知後端，告知它使用者正在手動恢復工作階段。

* _如果針對相同工作階段呼叫`trackSessionEnd`兩次，會發生什麼情況？_

  為相同工作階段多次呼叫`trackSessionEnd`是安全的。 後端會關閉第一個事件的工作階段，並自動捨棄該工作階段ID的所有後續事件，包括第二個`trackSessionEnd`。 這表示競爭條件（例如觀看者關閉播放器的同時觸發30分鐘非使用狀態逾時）不會產生重複資料。

* _如果工作階段處於作用中狀態時呼叫`trackSessionStart`，會發生什麼情況？_

  如果工作階段尚未關閉，SDK會忽略第二個`trackSessionStart`呼叫。 如果您需要啟動新的工作階段，請先呼叫`trackSessionEnd`以明確關閉目前的工作階段，然後呼叫新工作階段的`trackSessionStart`。
