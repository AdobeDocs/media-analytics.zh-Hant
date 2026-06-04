---
title: 隱藏式字幕總時間
description: 報告在工作階段期間啟用的累積秒數字幕。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---


# 隱藏式字幕總時間

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**隱藏式字幕總時間**報告量度。 請參閱[隱藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**隱藏式字幕總時間**&#x200B;量度會報告在工作階段期間啟用字幕的累積時間（以秒為單位）。 後端會加總啟用註解狀態開始與相符的狀態結束事件之間的每個間隔。

## 此量度的計算方式

媒體後端會加總工作階段中所有已啟用註解間隔的經過時間。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.closedcaptioning.time`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "closedCaptioning"`，欄位`time` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.time` |
