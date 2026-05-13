---
title: 掉格影響的資料流
description: 計算至少捨棄一個影格的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 9%

---


# 掉格影響的資料流

**掉格影響的資料流**&#x200B;量度會計算至少掉一個格的工作階段。 此量度是工作階段層級的布林值 — 在相同工作階段數內，發生多個卸除作為一個受影響的資料流。 若要取得總下拉音量，請使用[掉格](dropped-frames.md)。

## 此量度的計算方式

如果QoE物件的`droppedFrames`值在工作階段關閉時大於零，媒體後端會設定`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true`。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.droppedFrames`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
