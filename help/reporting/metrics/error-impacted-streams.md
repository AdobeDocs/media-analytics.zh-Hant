---
title: 錯誤影響的資料流
description: 計算至少發生一個錯誤的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# 錯誤影響的資料流

**錯誤影響的資料流**&#x200B;量度會計算至少發生一個錯誤（`trackError`已呼叫或[錯誤](/help/implementation/events/error.md)事件已觸發）的工作階段。 量度是工作階段層級的布林值 — 相同工作階段內的多個錯誤計為一個受影響的資料流。 若要取得總錯誤量，請使用[錯誤](/help/reporting/dimensions/errors.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到[錯誤](/help/implementation/events/error.md)事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.error`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
