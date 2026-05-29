---
title: 追蹤章節和區段
description: 如何使用 Media SDK 實作章節和區段追蹤。
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# 追蹤章節和區段

章節和區段追蹤適用於自訂的媒體章節或區段。 章節追蹤的一些常見用途是根據媒體內容 (例如棒球局次) 定義自訂區段，或定義廣告插播之間的內容區段。 核心媒體追蹤實作&#x200B;**不**&#x200B;需要章節追蹤。

章節追蹤包括章節開始、章節完成，以及章節略過。 使用具有自訂分段邏輯的媒體播放器API來識別章節事件並填入章節變數。

## 播放器事件

| 播放器事件 | 動作 |
| --- | --- |
| 章節開始 | 建立章節物件；呼叫ChapterStart |
| 章節完成 | 呼叫ChapterComplete |
| 章節略過 | 呼叫ChapterSkip |

## 實作步驟

1. 識別章節開始事件何時發生，並建立章節物件。 如需欄位定義，請參閱[章節名稱](/help/implementation/variables/chapters/chapter-name.md)、[章節位置](/help/implementation/variables/chapters/chapter-position.md)、[章節長度](/help/implementation/variables/chapters/chapter-length.md)和[章節位移](/help/implementation/variables/chapters/chapter-offset.md)。
1. 可選擇為自訂章節中繼資料建立內容資料變數。
1. 呼叫[章節開始](/help/implementation/events/chapters/chapter-start.md)以開始追蹤章節。
1. 當播放達到章節結束界限時，請呼叫[章節完成](/help/implementation/events/chapters/chapter-complete.md)。
1. 如果使用者在完成前略過章節，請呼叫[章節略過](/help/implementation/events/chapters/chapter-skip.md)。
1. 如需其他章節，請重複步驟1到5。
