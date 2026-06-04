---
title: 全熒幕次數
description: 報告檢視者在工作階段期間進入全熒幕的次數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# 全熒幕次數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**全熒幕計數**&#x200B;報告量度。 請參閱[全熒幕](/help/implementation/variables/player-state/full-screen.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**全熒幕計數**&#x200B;量度會報告檢視者在工作階段期間進入全熒幕的次數。 每個全熒幕狀態開始事件都會增加計數。 與受全熒幕影響的[串流](full-screen-streams-impacted.md)配對，以進行工作階段層級的布林值統計；與全熒幕總持續時間[&#128279;](full-screen-total-duration.md)配對，以進行狀態總時間。

## 此量度的計算方式

媒體後端會在每個全熒幕狀態開始事件上增加此計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.fullscreen.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "fullscreen"`，欄位`count` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
