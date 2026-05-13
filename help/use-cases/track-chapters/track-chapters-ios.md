---
title: 了解如何在 iOS 上追蹤章節和區段
description: 了解如何在 iOS 上使用 Media SDK 實作章節和區段追蹤。
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
exl-id: ea8a1dd6-043f-41a4-9cef-845da92bfa32
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xo94BYsFdo612h-FjNYkreRsjLC3lMYLXW-w-ltLkIE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 95%

---

# 在 iOS 上追蹤章節和區段{#track-chapters-and-segments-on-ios}

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

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME]
                        position:[POSITION]
                        length:[LENGTH]
                        startTime:[START_TIME]];
   ```

1. 如果您包含該章節的自訂中繼資料，請為中繼資料建立內容資料變數：

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init];
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"];
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"];
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. 若要開始追蹤章節播放，請呼叫 `ChapterStart` 例項中的 `MediaHeartbeat` 事件：

   ```
   - (void)onChapterStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary];
   }
   ```

1. 當播放達到由您的自訂程式碼定義之章節結束界限時，請呼叫 `ChapterComplete` 例項中的 `MediaHeartbeat` 事件：

   ```
   - (void)onChapterComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. 如果因為使用者選擇略過章節而未完成章節播放 (例如，如果使用者搜尋超出章節界限)，請呼叫 MediaHeartbeat 例項中的 `ChapterSkip` 事件：

   ```
   - (void)onChapterSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. 如果有任何其他章節，請重複步驟 1 到 5。
