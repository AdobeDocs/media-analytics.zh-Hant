---
title: 廣告逗留時間
description: 報告每個工作階段作用中廣告播放的總秒數。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---


# 廣告逗留時間

**廣告逗留時間**&#x200B;量度會報告每個工作階段作用中廣告播放的總秒數，但不包括暫停、緩衝和停頓。 配對[內容逗留時間](/help/reporting/metrics/content-time-spent.md)，比較廣告載入與內容參與度。

## 此量度的計算方式

當播放器處於廣告上的`play`狀態時，媒體後端會加總兩個事件之間經過的時鐘時間。 暫停期間、緩衝期間和搜尋期間的時間會被排除，這與[主要內容花費的內容時間](/help/reporting/metrics/content-time-spent.md)的計算方式一致。 量度會在廣告關閉呼叫上報告。 值在Analysis Workspace中顯示為`HH:MM:SS`，在資料摘要、Data Warehouse及報表API中以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.timePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
