---
title: 內容完成
description: 計算播放點達到內容結尾的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---


# 內容完成

**內容完成**&#x200B;量度會計算播放點到達內容結尾的工作階段。 配對[Content starts](content-starts.md)以計算完成率；配對[Media starts](media-starts.md)以計算端對端檢視率。

## 此量度的計算方式

媒體後端在收到[工作階段完成](/help/implementation/events/session/session-complete.md)事件時設定此旗標。 量度會在關閉呼叫時回報。 在沒有明確`sessionComplete`的情況下逾時的工作階段不會計為完成。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.complete`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.complete` |
