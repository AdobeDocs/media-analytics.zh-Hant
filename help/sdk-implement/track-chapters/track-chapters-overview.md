---
seo-title: 概述
title: 概述
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 概述{#overview}

>[!IMPORTANT]
>
>以下說明提供使用2.x SDK實作的指引。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

章節和區段追蹤適用於自訂定義的媒體章節或區段。 章節追蹤的常見用途，是根據媒體內容（例如棒球注入）定義自訂區段，或在廣告插播之間定義內容區段。 Chapter tracking is **not** required for core media tracking implementations.

章節追蹤包括章節開始、章節完成，以及章節略過。您可將媒體播放器API與自訂的分段邏輯搭配使用，以識別章節事件並填入必要和選用的章節變數。

## 播放器事件

### 在章節開始時

* 建立章節的章節物件例項，`chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 在章節完成時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 在章節略過時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## 實施章節追蹤 {#implement-chapter-tracking}

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   以下是 `ChapterObject` 章節追蹤參考:

   >[!NOTE]
   >
   >只有在您打算追蹤章節時，才需要這些變數。

   | 變數名稱 | 說明 | 必要 |
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

下列范常式式碼使用JavaScript 2.x SDK做為HTML5媒體播放器。 您應將此程式碼與核心媒體播放程式碼搭配使用。

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

