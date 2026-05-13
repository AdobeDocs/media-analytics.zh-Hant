---
title: 受觀看中影響的資料流
description: 至少計算一次播放器處於焦點的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# 受觀看中影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受焦點影響的&#x200B;**資料流**報告量度。 請參閱[焦點](/help/implementation/variables/player-state/in-focus.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

受觀看中影響的&#x200B;**資料流**&#x200B;量度會計入播放器至少有一次觀看中的工作階段。 量度是工作階段層級的布林值 — 相同工作階段中的多個焦點事件會計為一個受影響的資料流。 若要取得焦點事件數量總計，請使用[焦點計數](in-focus-count.md)。

## 此量度的計算方式

媒體後端在第一次收到`statesStart`中具有`inFocus`的`media.statesUpdate`事件時，將`inFocus`專案的`mediaReporting.states[]`中的`isSet`旗標設為`true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.infocus.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "inFocus"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
