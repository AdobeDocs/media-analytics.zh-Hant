---
title: 了解如何使用 JavaScript 2.x 追蹤章節和區段
description: 了解如何在瀏覽器應用程式 (JS) 中使用 Media SDK 實作章節和區段追蹤。
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
exl-id: 9964ec0c-cce9-4ccc-bd26-a2b3fcdc3e28
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '198'
ht-degree: 100%

---

# 使用 JavaScript 2.x 追蹤章節和區段{#track-chapters-and-segments-on-javascript}

下列指示提供使用 2.x SDK 實作的指引。

>[!IMPORTANT]
>
> 若您正在實作 SDK 1.x 版，您可以在此處下載開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   `ChapterObject` 章節追蹤參考資料：

   >[!NOTE]
   >
   >唯有在您計劃追蹤章節時，才須使用這些變數。

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 章節名稱 | 是 |
   | `position` | 章節位置 | 是 |
   | `length` | 章節長度 | 是 |
   | `startTime` | 章節開始時間 | 是 |

   章節物件：

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. 如果您包含該章節的自訂中繼資料，請為中繼資料建立內容資料變數：

   ```js
   var chapterCustomMetadata = {
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info"
   };
   ```

1. 若要開始追蹤章節播放，請呼叫 `ChapterStart` 例項中的 `MediaHeartbeat` 事件：

   ```js
   _onChapterStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata);
   };
   ```

1. 當播放達到由您的自訂程式碼定義之章節結束界限時，請呼叫 `ChapterComplete` 例項中的 `MediaHeartbeat` 事件：

   ```js
   _onChapterComplete = function() {
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   };
   ```

1. 如果因為使用者選擇略過章節而未完成章節播放 (例如，如果使用者搜尋超出章節界限)，請呼叫 MediaHeartbeat 例項中的 `ChapterSkip` 事件：

   ```js
   _onChapterSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   };
   ```

1. 如果有任何其他章節，請重複步驟 1 到 5。
