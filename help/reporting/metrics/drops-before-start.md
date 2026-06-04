---
title: 開始前掉格
description: 計算檢視器在任何主要內容轉譯前結束的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# 開始前掉格

**開始前掉格**&#x200B;量度會計算檢視器在轉譯任何主要內容前結束的工作階段。 此量度會無論廣告行為如何，標示預先內容捨棄，因此是單純預先內容捨棄的最佳量度。 將其與[媒體開始](/help/reporting/metrics/media-starts.md)和[內容開始](/help/reporting/metrics/content-starts.md)配對，以計算從未產生內容框架的工作階段共用。

## 此量度的計算方式

媒體後端會為關閉的工作階段設定此旗標，而不會在主內容上產生[播放](/help/implementation/events/playback/play.md)事件。 量度會在關閉呼叫時回報。 常見的情況包括：檢視器在前段廣告期間退出、播放器在初始緩衝階段無限期停頓，或是在第一個主要內容播放事件之前引發錯誤。 在這些情況下，工作階段會記錄[媒體開始](/help/reporting/metrics/media-starts.md)，但沒有[內容開始](/help/reporting/metrics/content-starts.md)，而且沒有記錄[進度標籤](/help/reporting/metrics/progress-markers.md)。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.dropBeforeStart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
