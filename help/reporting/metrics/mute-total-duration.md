---
title: 靜音總時間
description: 報告在工作階段期間音訊被靜音的累積秒數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 7%

---


# 靜音總時間

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**靜音總持續時間**報告量度。 請參閱[靜音](/help/implementation/variables/player-state/mute.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**靜音總持續時間**&#x200B;量度會報告在工作階段期間將音訊靜音的累積時間（以秒為單位）。 後端會加總靜音狀態 — 開始與相符狀態 — 結束事件之間的每個間隔。

## 此量度的計算方式

媒體後端會加總工作階段期間所有靜音間隔的經過時間。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.mute.time`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "mute"`，欄位`time` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
