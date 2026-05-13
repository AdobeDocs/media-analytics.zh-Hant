---
title: 不重複播放時間
description: 報告工作階段期間檢視的不同內容的秒數，去除重複的搜尋回放次數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 不重複播放時間

**不重複播放時間**&#x200B;量度會報告工作階段期間檢視的不同內容的秒數，刪除透過向後搜尋重播的重複區段。 與[內容逗留時間](content-time-spent.md)相比，當檢視者在相同工作階段中重新觀看相同內容的一部分時，不重複播放時間會較低。

## 此量度的計算方式

媒體後端會追蹤在工作階段期間檢視了哪些播放點間隔，並加總其聯合。 播放同一個5秒區段兩次，仍會計為5秒。 量度會在關閉呼叫時回報。 值在Analysis Workspace中顯示為`HH:MM:SS`，在資料摘要、Data Warehouse及報表API中以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.uniqueTimePlayed`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
