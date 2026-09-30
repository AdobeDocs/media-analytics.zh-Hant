---
title: 廣告完成
description: 計算每個播放到完成的廣告。
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
source-wordcount: '123'
ht-degree: 12%
---

# 廣告完成

**廣告完成**&#x200B;量度會計算每個播放到完成的廣告。 將其與[廣告開始](ad-starts.md)配對，以計算廣告完成率。

## 此量度的計算方式

媒體後端在收到[廣告完成](/help/implementation/events/ads/ad-complete.md)事件時設定此旗標。 量度會在廣告關閉呼叫上報告。 略過或捨棄的廣告不會計為完成。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.ad.complete`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
