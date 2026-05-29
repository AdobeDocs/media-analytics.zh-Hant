---
title: 內容開始
description: 計算主要內容實際開始播放的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# 內容開始

**內容開始**&#x200B;量度會計算主要內容實際開始播放的工作階段。 與[媒體開始](media-starts.md)不同，它排除在前段廣告、緩衝或停頓期間結束的工作階段。 這使得它成為完成率和參與率的正確分母。

## 此量度的計算方式

媒體後端在第一次收到主要內容的[播放](/help/implementation/events/playback/play.md)事件時設定此旗標。 量度會在該播放事件上觸發，但在關閉呼叫上報告。 若要計算前段下拉率，請使用`(Media starts − Content starts) / Media starts`。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.play`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.play` |
