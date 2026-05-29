---
title: 媒體開始
description: 計算開始的每個媒體工作階段，包括以前段廣告或緩衝結束的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# 媒體開始

**媒體開始**&#x200B;量度會計算每個開始的媒體工作階段。 後端一收到[工作階段開始](/help/implementation/events/session/session-start.md)事件時，即使檢視器在前段廣告、緩衝或任何主要內容播放之前退出，也會遞增。 將它當做媒體報表最廣泛的funnel頂端量度；將其與[Content starts](content-starts.md)配對，以測量廣告和緩沖流失。

## 此量度的計算方式

媒體後端在收到[工作階段開始](/help/implementation/events/session/session-start.md)事件時設定此旗標。 報告的量度是每個工作階段`1`。 媒體開始次數是報告於開始呼叫，而非關閉呼叫；這是唯一不會等待工作階段關閉的量度。 所有其他媒體量度，包括[內容開始](/help/reporting/metrics/content-starts.md)、[內容逗留時間](/help/reporting/metrics/content-time-spent.md)和[進度標籤](/help/reporting/metrics/progress-markers.md)，都會在關閉通話時回報，並且在播放期間無法即時使用。 [廣告開始](/help/reporting/metrics/ad-starts.md)是在其觸發事件上報告的一個額外的量度，而不是在關閉時。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.view`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.view` |
