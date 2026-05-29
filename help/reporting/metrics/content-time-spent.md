---
title: 內容逗留時間
description: 報告每個工作階段作用中主要內容播放的總秒數。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 6%

---


# 內容逗留時間

**內容逗留時間**&#x200B;量度會報告每個工作階段作用中主要內容播放的總秒數，不包括廣告、暫停、緩衝和停頓。 將其用作內容檢視的參與量度；如需包含廣告的逗留時間，請參閱[媒體逗留時間](media-time-spent.md)。

## 此量度的計算方式

當播放器處於主要內容的`play`狀態時，媒體後端會加總事件之間經過的時鐘時間。 會排除廣告、暫停、緩衝事件和停頓的時間。 因為只計算作用中播放時間，所以當檢視器向後搜尋並重新觀看區段時，量度可能會超過[內容長度](/help/reporting/dimensions/content-length.md)。 每個通過指定區段的過程都會累積額外的播放時間，而且只要使用者消耗工作階段中的內容並倒轉內容，就會累積。 量度會在關閉呼叫時回報。 值在Analysis Workspace中顯示為`HH:MM:SS`，在資料摘要、Data Warehouse及報表API中以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.timePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
