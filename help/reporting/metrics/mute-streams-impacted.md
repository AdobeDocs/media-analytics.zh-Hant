---
title: 受靜音影響的資料流
description: 計算檢視器至少將音訊靜音一次的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# 受靜音影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受靜音影響的&#x200B;**資料流**&#x200B;報告量度。 請參閱[靜音](/help/implementation/variables/player-state/mute.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

受靜音影響的&#x200B;**資料流**&#x200B;量度會計入檢視器至少將音訊靜音一次的工作階段。 量度是工作階段層級的布林值 — 在相同工作階段中，將多個靜音切換為一個受影響的資料流。 若要取得靜音音量總計，請使用[靜音計數](mute-count.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到靜音狀態開始事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.mute.set`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "mute"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
