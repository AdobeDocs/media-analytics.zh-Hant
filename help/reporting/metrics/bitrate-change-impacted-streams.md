---
title: 位元速率變更影響的資料流
description: 計算至少發生一個位元速率變更的工作階段。
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
source-wordcount: '145'
ht-degree: 10%
---

# 位元速率變更影響的資料流

**位元速率變更影響的資料流**&#x200B;量度會計算至少發生一次位元速率變更的工作階段。 量度是工作階段層級的布林值；相同工作階段中的多個位元速率變更會計為一個受影響的資料流。 若要取得位元速率變更磁碟區總數，請使用[位元速率變更](/help/reporting/dimensions/bitrate-changes.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到[位元速率變更](/help/implementation/events/playback/bitrate-change.md)事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.bitrateChange`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
