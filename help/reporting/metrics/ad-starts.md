---
title: 廣告開始
description: 計算工作階段期間開始播放的每個廣告數。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---


# 廣告開始

**廣告開始**&#x200B;量度會計入工作階段期間開始播放的每個廣告。 請將其與[廣告完成](ad-completes.md)配對，以計算廣告完成率，並與[廣告計數](/help/reporting/metrics/ad-count.md)進行對等的工作階段層級統計。

## 此量度的計算方式

收到[廣告開始](/help/implementation/events/ads/ad-start.md)事件時，媒體後端會設定`mediaReporting.advertisingDetails.isStarted = true`。 量度會在廣告開始呼叫上報告。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.view`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.ad.view` |
