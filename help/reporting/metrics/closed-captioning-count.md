---
title: 隱藏式字幕次數
description: 報告檢視者在工作階段期間啟用字幕的次數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# 隱藏式字幕次數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**隱藏式字幕計數**&#x200B;報告量度。 請參閱[隱藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**隱藏式字幕計數**&#x200B;量度會報告檢視者在工作階段期間啟用字幕的次數。 每個註解啟用狀態開始事件都會增加計數。 配對[個受隱藏式字幕影響的資料流](closed-captioning-streams-impacted.md) （用於工作階段層級的布林值統計）和[隱藏式字幕總持續時間](closed-captioning-total-duration.md) （用於狀態總時間）。

## 此量度的計算方式

媒體後端會遞增每個註解啟用狀態開始事件的計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.closedcaptioning.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "closedCaptioning"`，欄位`count` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
