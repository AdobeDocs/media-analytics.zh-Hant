---
title: 總暫停期間
description: 報告檢視者在工作階段期間暫停的累積秒數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# 總暫停期間

**總暫停期間**&#x200B;量度會報告檢視者在工作階段期間暫停的累積秒數。 此量度是每個[暫停開始](/help/implementation/events/playback/pause-start.md)事件與後續[播放](/help/implementation/events/playback/play.md)事件之間的所有間隔總和。 多個暫停會相加。 與[暫停事件](pause-events.md)配對，以匯出平均暫停長度。

## 此量度的計算方式

媒體後端會加總每[暫停開始](/help/implementation/events/playback/pause-start.md)事件和相符的[播放](/help/implementation/events/playback/play.md)事件之間經過的時鐘時間。 量度會在關閉呼叫時回報。 該值在Analysis Workspace中會顯示為`HH:MM:SS`，在其他地方則會以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.pauseTime`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
