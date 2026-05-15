---
title: 觀看中次數
description: 報告播放器在工作階段期間獲得焦點的次數。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# 觀看中次數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**觀看中計數**報告量度。 請參閱[焦點](/help/implementation/variables/player-state/in-focus.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**觀看中計數**&#x200B;量度會報告播放器在工作階段期間獲得觀看中焦點的次數。 每個焦點狀態開始事件都會增加計數。 與工作階段層級布林值統計中受焦點影響的[資料流](in-focus-streams-impacted.md)配對，與處於狀態總時間的[焦點總持續時間](in-focus-total-duration.md)配對。

## 此量度的計算方式

媒體後端會遞增每個焦點狀態開始事件上`mediaReporting.states[]`之`inFocus`專案中的`count`欄位。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.infocus.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "inFocus"`，欄位`count` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
