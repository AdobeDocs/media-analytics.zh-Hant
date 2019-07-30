---
seo-title: 概述
title: 概述
uuid: 3Fe32425-5e2a -4886-fea-d91 d15671 bb0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 概述{#overview}

>[!IMPORTANT]
>
>下列指示提供使用2.x SDK進行實施的指引。If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

章節和區段追蹤適用於自訂的媒體章節或區段。章節追蹤的一些常見用法是根據媒體內容(例如棒球傳入)定義自訂群體，或在廣告插播之間定義內容區段。Chapter tracking is **not** required for core media tracking implementations.

章節追蹤包括章節開始、章節完成，以及章節略過。您可以使用媒體播放器API搭配自訂分段邏輯來識別章節事件，以及填入必要和選擇性的章節變數。

## 播放器事件

### 在章節開始時

* 建立章節的章節物件例項，`chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 在章節完成時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 在章節略過時

* 呼叫 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   以下是 `ChapterObject` 章節追蹤參考:

   >[!NOTE]
   >
   >只有當您打算追蹤章節時，才需要這些變數。

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

下列範例程式碼使用HTML媒體播放器的JavaScript2.x SDK。您應使用此程式碼搭配核心媒體播放程式碼。

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

## 驗證 {#section_07EC2811BE3249249494596BFE9BF869}

### 章節開始

在個別章節播放開始時，會傳送一個關鍵呼叫：

* 心率章節開始(此呼叫包含其他章節中繼資料變數)。

### 章節完成

在章節界限結束時，將傳送心率章節完成呼叫。

### 章節略過

略過章節時，將傳送心率章節略過呼叫。
