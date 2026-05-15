---
title: 了解如何追蹤已說明的章節和區段
description: 如何使用 Media SDK 實作章節和區段追蹤。
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 95%

---

# 概觀{#overview}

下列指示提供使用 2.x SDK 實作的指引。

>[!IMPORTANT]
> 
> 若您正在實作 SDK 1.x 版，您可以在此處下載開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

章節和區段追蹤適用於自訂的媒體章節或區段。 章節追蹤的一些常見用途是根據媒體內容 (例如棒球局次) 定義自訂區段，或定義廣告插播之間的內容區段。 核心媒體追蹤實作&#x200B;**不**&#x200B;需要章節追蹤。

章節追蹤包括章節開始、章節完成，以及章節略過。 您可以使用具有自訂區段邏輯的媒體播放器 API 來識別章節事件，並填入必要和選用的章節變數。

## 播放器事件

### 在章節開始時

* 建立章節的章節物件例項，`chapterObject`
* 填入章節中繼資料，`chapterCustomMetadata`
* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 在章節完成時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 在章節略過時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## 實作章節追蹤 {#implement-chapter-tracking}

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   以下是 `ChapterObject` 章節追蹤參考：

   >[!NOTE]
   >
   >唯有在您計劃追蹤章節時，才須使用這些變數。

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 章節名稱 | 是 |
   | `position` | 章節位置 | 是 |
   | `length` | 章節長度 | 是 |
   | `startTime` | 章節開始時間 | 是 |

1. 如果您包含該章節的自訂中繼資料，請為中繼資料建立內容資料變數。
1. 若要開始追蹤章節播放，請呼叫 `ChapterStart` 例項中的 `MediaHeartbeat` 事件.
1. 當播放達到由您的自訂程式碼定義之章節結束界限時，請呼叫 `ChapterComplete` 例項中的 `MediaHeartbeat` 事件.
1. 如果因為使用者選擇略過章節而未完成章節播放 (例如，如果使用者搜尋超出章節界限)，請呼叫 MediaHeartbeat 例項中的 `ChapterSkip` 事件.
1. 如果有任何其他章節，請重複步驟 1 到 5。

以下程式碼範例將 JavaScript 2.x SDK 用於 HTML5 媒體播放器。 您應該將此程式碼與核心媒體播放程式碼一起使用。

```js
/* Call on chapter start */
if (e.type == "chapter start") {
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500);
    /* Set custom context data*/
    var chapterCustomMetadata = {
        segmentType:"Baseball Innings",
        segmentName:"Inning 5",
        segmentInfo:"Game Six"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata);
};

/* Call on chapter complete */
if (e.type == "chapter complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};

/* Call on chapter skip */
if (e.type == "chapter skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

>[!MORELIKETHIS]
>
>* [章節開始](/help/implementation/events/chapters/chapter-start.md)
>* [章節完成](/help/implementation/events/chapters/chapter-complete.md)
>* [章節略過](/help/implementation/events/chapters/chapter-skip.md)
