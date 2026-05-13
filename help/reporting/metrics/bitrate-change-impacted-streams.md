---
title: 位元速率變更影響的資料流
description: 計算至少發生一個位元速率變更的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# 位元速率變更影響的資料流

**位元速率變更影響的資料流**&#x200B;量度會計算至少發生一次位元速率變更的工作階段。 量度是工作階段層級的布林值 — 相同工作階段內的多個位元速率變更會計為一個受影響的資料流。 若要取得位元速率變更磁碟區總數，請使用[位元速率變更](/help/reporting/dimensions/bitrate-changes.md)。

## 此量度的計算方式

媒體後端在工作階段期間第一次收到`media.bitrateChange`事件時設定`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bitrateChange`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
