---
title: 緩衝影響的資料流
description: 計算播放器至少一次進入緩衝狀態的工作階段。
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
source-wordcount: '147'
ht-degree: 10%
---

# 緩衝影響的資料流

**緩衝影響的資料流**&#x200B;量度會計算播放器至少一次進入緩衝狀態的工作階段。 量度是工作階段層級的布林值；相同工作階段中的多個緩衝事件會計為一個受影響的資料流。 若要取得總緩衝區磁碟區，請使用[緩衝區事件](buffer-events.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到[緩衝開始](/help/implementation/events/playback/buffer-start.md)事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.buffer`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
