---
title: 章節逗留時間
description: 報告每個章節的使用中播放的總秒數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# 章節逗留時間

**章節逗留時間**&#x200B;量度會報告每個章節的使用中播放總秒數。 配對[章節長度](/help/reporting/dimensions/chapter-length.md)以計算每個使用章節的分享。

## 此量度的計算方式

當播放器處於章節上的`play`狀態時，媒體後端會加總事件之間經過的時鐘時間。 暫停期間、緩衝期間和停止期間的時間會被排除。 量度會在章節關閉呼叫上報告。 值在Analysis Workspace中顯示為`HH:MM:SS`，在資料摘要、Data Warehouse及報表API中以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體章節]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.chapter.timePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
