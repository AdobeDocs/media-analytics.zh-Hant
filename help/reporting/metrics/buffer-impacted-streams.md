---
title: 緩衝影響的資料流
description: 計算播放器至少一次進入緩衝狀態的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# 緩衝影響的資料流

**緩衝影響的資料流**&#x200B;量度會計算播放器至少一次進入緩衝狀態的工作階段。 量度是工作階段層級的布林值 — 在相同工作階段中，多個緩衝事件會計為單一受影響的資料流。 若要取得總緩衝區磁碟區，請使用[緩衝區事件](buffer-events.md)。

## 此量度的計算方式

媒體後端在工作階段期間第一次收到`media.bufferStart`事件時設定`mediaReporting.qoeDataDetails.hasBufferImpactedStreams = true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.buffer`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
