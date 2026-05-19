---
title: 延遲受影響的串流
description: 計算播放期間發生至少一個停頓的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# 延遲受影響的串流

**Stall影響的資料流**&#x200B;量度會計算播放期間至少發生一次停頓的工作階段。 量度是工作階段層級的布林值 — 相同工作階段內的多個停止計為一個受影響的資料流。 若要取得總停止數量，請使用[停止事件](stall-events.md)。

## 此量度的計算方式

在工作階段期間，當主要內容上至少連續三個事件沒有記錄播放點移動時，媒體後端會設定`mediaReporting.qoeDataDetails.hasStallImpactedStreams = true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.qoe.stall`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.qoe.stall`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
