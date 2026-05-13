---
title: 章節完成
description: 計算每個播放到結束的章節。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# 章節完成

**章節完成**&#x200B;量度會計算每個播放到完成的章節。 將其與[章節開始](chapter-starts.md)配對，以計算章節完成率。

## 此量度的計算方式

收到`media.chapterComplete`事件時，媒體後端會設定`mediaReporting.chapterDetails.isCompleted = true`。 量度會在章節關閉呼叫上報告。 在播放中跳過或放棄的章節不計為完成。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體章節]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.chapter.complete`收集。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
