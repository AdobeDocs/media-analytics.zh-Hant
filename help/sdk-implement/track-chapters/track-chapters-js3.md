---
title: 使用JavaScript 3.x追蹤章節和區段
description: 本主題說明如何在瀏覽器應用程式 (JS) 中使用 Media SDK 實作章節和區段追蹤。
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---


# 使用JavaScript 3.x追蹤章節和區段{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>下列指示提供使用 3.x SDK 實作的指引。If you are implementing any previous versions of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   `ChapterObject` 章節追蹤參考資料:

   >[!NOTE]
   >
   >唯有在您計劃追蹤章節時，才須使用這些變數。

   | 變數名稱 | 類型 | 說明 |
   | --- | --- | --- |
   | `name` | string | 表示章節名稱的非空字串。 |
   | `position` | 數字 | 章節在內容中的位置，從1開始。 |
   | `length` | 數字 | 表示章節長度的正數。 |
   | `startTime` | 數字 | 章節開頭的Playhead值。 |

   章節物件:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. 如果您包含該章節的自訂中繼資料，請為中繼資料建立內容資料變數:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. 若要開始追蹤章節播放，請呼叫 `ChapterStart` 例項中的 `MediaHeartbeat` 事件:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. 當播放達到由您的自訂程式碼定義之章節結束界限時，請呼叫 `ChapterComplete` 例項中的 `MediaHeartbeat` 事件:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. 如果因為使用者選擇略過章節而未完成章節播放 (例如，如果使用者搜尋超出章節界限)，請呼叫 MediaHeartbeat 例項中的 `ChapterSkip` 事件:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. 如果有任何其他章節，請重複步驟 1 到 5。
