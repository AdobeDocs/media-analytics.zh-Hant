---
title: 總暫停期間
description: 報告檢視者在工作階段期間暫停的累積秒數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 8%

---


# 總暫停期間

**總暫停期間**&#x200B;量度會報告檢視者在工作階段期間暫停的累積秒數。 量度是每個`media.pauseStart`與後續`media.play`之間所有間隔的總和。 多個暫停會相加。 與[暫停事件](pause-events.md)配對，以匯出平均暫停長度。

## 此量度的計算方式

媒體後端加總每`media.pauseStart`和相符的`media.play`事件之間經過的時鐘時間。 量度會在關閉呼叫時回報。 該值在Analysis Workspace中會顯示為`HH:MM:SS`，在其他地方則會以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.pauseTime`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
