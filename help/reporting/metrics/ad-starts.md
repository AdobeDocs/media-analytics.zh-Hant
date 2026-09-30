---
title: 廣告開始
description: 計算工作階段期間開始播放的每個廣告數。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%
---

# 廣告開始

**廣告開始**&#x200B;量度會計入工作階段期間開始播放的每個廣告。 請將其與[廣告完成](ad-completes.md)配對，以計算廣告完成率，並與[廣告計數](/help/reporting/metrics/ad-count.md)進行對等的工作階段層級統計。

## 此量度的計算方式

媒體後端在收到[廣告開始](/help/implementation/events/ads/ad-start.md)事件時設定此旗標。 量度會在廣告開始呼叫上報告。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.ad.view`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.ad.view` |
