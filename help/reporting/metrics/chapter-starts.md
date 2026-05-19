---
title: 章節開始
description: 計算工作階段期間開始播放的每個章節。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# 章節開始

**章節開始**&#x200B;量度會計算工作階段期間開始播放的每個章節。 將其與[章節完成](chapter-completes.md)配對，以計算章節完成率。

## 此量度的計算方式

當收到[章節開始](/help/implementation/events/chapters/chapter-start.md)事件時，媒體後端會設定此旗標。 量度會在章節關閉呼叫上報告。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體章節]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.chapter.view`收集。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
