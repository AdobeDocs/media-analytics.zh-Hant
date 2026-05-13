---
title: 受全熒幕影響的資料流
description: 計算檢視器至少一次進入全熒幕的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 受全熒幕影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受全熒幕&#x200B;**報告量度影響的**資料流。 請參閱[全熒幕](/help/implementation/variables/player-state/full-screen.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

受全熒幕影響的&#x200B;**串流**&#x200B;量度會計入檢視器至少一次進入全熒幕的工作階段。 量度是工作階段層級的布林值 — 相同工作階段中的多個全熒幕專案會計為一個受影響的資料流。 若要取得全熒幕輸入音量，請使用[全熒幕計數](full-screen-count.md)。

## 此量度的計算方式

媒體後端在第一次收到`statesStart`中具有`fullscreen`的`media.statesUpdate`事件時，將`fullscreen`專案的`mediaReporting.states[]`中的`isSet`旗標設為`true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.fullscreen.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "fullscreen"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
