---
title: 暫停事件
description: 計算工作階段期間發生的每個不同暫停次數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# 暫停事件

**暫停事件**&#x200B;量度會計算工作階段期間收到的每個不同[暫停開始](/help/implementation/events/playback/pause-start.md)事件，包括相同工作階段內的多次暫停。 請將其與[總暫停期間](total-pause-duration.md)配對，以匯出平均暫停長度，並與[受暫停影響的資料流](paused-impacted-streams.md)配對，以計算至少暫停一次的工作階段。

## 此量度的計算方式

媒體後端會在每[個暫停開始](/help/implementation/events/playback/pause-start.md)事件時增加此計數。 單一連續暫停會產生一個增量，無論其持續時間為何。 在播放器保持暫停狀態時傳送的心率[Ping](/help/implementation/events/playback/ping.md)全都屬於相同的暫停期間，不會再次增加計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.pauseCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
