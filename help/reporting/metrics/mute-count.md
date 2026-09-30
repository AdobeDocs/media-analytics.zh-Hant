---
title: 靜音次數
description: 報告檢視者在工作階段期間將音訊靜音的次數。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%
---

# 靜音次數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**靜音計數**報告量度。 請參閱[靜音](/help/implementation/variables/player-state/mute.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**靜音計數**&#x200B;量度會報告檢視者在工作階段期間將音訊靜音的次數。 每個靜音狀態開始事件都會增加計數。 配對[受靜音影響的資料流](mute-streams-impacted.md)以進行工作階段層級的布林值統計，配對[靜音總持續時間](mute-total-duration.md)以進行狀態總時間。

## 此量度的計算方式

媒體後端會在每個靜音狀態開始事件上增加此計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.mute.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "mute"`，欄位`count` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
