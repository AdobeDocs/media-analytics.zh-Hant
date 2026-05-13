---
title: 廣告完成
description: 計算每個播放到完成的廣告。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# 廣告完成

**廣告完成**&#x200B;量度會計算每個播放到完成的廣告。 將其與[廣告開始](ad-starts.md)配對，以計算廣告完成率。

## 此量度的計算方式

收到`media.adComplete`事件時，媒體後端會設定`mediaReporting.advertisingDetails.isCompleted = true`。 量度會在廣告關閉呼叫上報告。 略過或捨棄的廣告不會計為完成。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.complete`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
