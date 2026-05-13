---
title: 章節
description: 報告每個已播放的唯一章節，並以自動產生的章節ID作為索引鍵。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---


# 章節

**Chapter**&#x200B;維度會報告每個已播放的唯一章節，並以自動產生的章節ID作為索引鍵。 ID是由SDK或後端從內容ID、章節索引和章節開始時間建構，因此相同內容上相同章節的兩個工作階段會統計為單一條列專案。 使用維度作為章節層級分類的聯結索引鍵，例如章節名稱、章節長度、章節位移和章節位置。

## 如何填入此維度

`media.chapterStart`引發時，會自動產生章節識別碼。 值不會直接設定；它是從章節位置、位移和內容ID衍生而來。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體章節]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.chapter.name`收集。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料饋送 | `videochapter, post_videochapter` |

## 維度項目

每個專案都是唯一的章節ID。 ID不透明（通常是內容ID +索引+位移的雜湊），並且最適合作為分組索引鍵。 與[章節名稱](chapter-name.md)配對，以取得易記標籤。
