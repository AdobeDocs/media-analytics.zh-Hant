---
title: 季數
description: 報告偶發內容的季數。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---


# 季數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**季**&#x200B;報告維度。 請參閱[季](/help/implementation/variables/standard-metadata/season.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**季節**&#x200B;維度會報告偶發內容的季數。 將它與[節目](show.md)和[集數](episode.md)搭配使用，以取得完整的集數劃分。

## 如何填入此維度

當內容為一系列當中的一部分時，播放器會在工作階段開始時設定季數。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.season`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoseason, post_videoseason` |

## 維度項目

每個專案是在工作階段開始時所報告的常值季節值（通常是字串整數，例如`"1"`、`"2"`）。 相同節目內的所有集數保持一致；維度不會將`"1"`和`"01"`標準化為相同的條列專案。
