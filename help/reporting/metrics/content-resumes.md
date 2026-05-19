---
title: 內容繼續
description: 計算繼續先前中斷之播放的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 9%

---


# 內容繼續

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容繼續**報告量度。 請參閱[內容履歷](/help/implementation/variables/core/content-resumes.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Content繼續**&#x200B;量度會計算繼續先前中斷之播放的工作階段。 當播放器將工作階段標示為`sessionStart`上的恢復時（例如，在緩衝、暫停或停止超過30分鐘後），它會遞增。 用它來區分相同檢視器和資產的正版新工作階段和後續工作階段。

## 此量度的計算方式

當`mediaCollection.sessionDetails.hasResume`在[工作階段開始](/help/implementation/events/session/session-start.md)事件上為`true`時，媒體後端會設定此旗標。 播放器必須將工作階段明確標幟為繼續。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.resume`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
