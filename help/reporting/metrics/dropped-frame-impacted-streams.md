---
title: 掉格影響的資料流
description: 計算至少捨棄一個影格的工作階段數。
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
source-wordcount: '135'
ht-degree: 11%
---

# 掉格影響的資料流

**掉格影響的資料流**&#x200B;量度會計算至少掉一個格的工作階段。 此量度是工作階段層級的布林值；相同工作階段內的多個資料捨棄計為一個受影響的資料流。 若要取得總下拉音量，請使用[掉格](dropped-frames.md)。

## 此量度的計算方式

如果QoE物件的`droppedFrames`值在工作階段關閉時大於零，媒體後端會設定此旗標。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.droppedFrames`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
