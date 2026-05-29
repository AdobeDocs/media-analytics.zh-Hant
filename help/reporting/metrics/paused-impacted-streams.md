---
title: 暫停的受影響串流
description: 計算檢視器至少暫停一次的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 11%

---


# 暫停的受影響串流

**暫停的受影響資料流**&#x200B;量度會計算檢視器至少暫停一次的工作階段。 這是工作階段層級的布林值。 相同工作階段內的多次暫停會計為一個受影響的資料流。 用它來測量經歷任何暫停的工作階段比例；若要取得總暫停數量，請使用[暫停事件](pause-events.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到[暫停開始](/help/implementation/events/playback/pause-start.md)事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.pause`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
