---
title: 在 JavaScript 上追蹤章節和區段
description: 本主題說明在瀏覽器應用程式(JS)中使用Media SDK實作章節和區段追蹤。
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 上追蹤章節和區段{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>以下說明提供使用2.x SDK實作的指引。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. 識別章節開始事件何時發生，並使用章節資訊建立 `ChapterObject` 例項。

   `ChapterObject` 章節追蹤參考：

   >[!NOTE]
   >
   >只有在您打算追蹤章節時，才需要這些變數。

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 章節名稱 | 是 |
   | `position` | 章節位置 | 是 |
   | `length` | 章節長度 | 是 |
   | `startTime` | 章節開始時間 | 是 |

   章節物件:

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. 如果您包含該章節的自訂中繼資料，請為中繼資料建立內容資料變數:

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. 若要開始追蹤章節播放，請呼叫 `ChapterStart` 例項中的 `MediaHeartbeat` 事件:

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. 當播放達到由您的自訂程式碼定義之章節結束界限時，請呼叫 `ChapterComplete` 例項中的 `MediaHeartbeat` 事件:

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. 如果因為使用者選擇略過章節而未完成章節播放 (例如，如果使用者搜尋超出章節界限)，請呼叫 MediaHeartbeat 例項中的 `ChapterSkip` 事件:

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. 如果有任何其他章節，請重複步驟 1 到 5。

