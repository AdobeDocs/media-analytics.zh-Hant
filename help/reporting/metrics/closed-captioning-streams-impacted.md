---
title: 受隱藏式字幕影響的資料流
description: 計算檢視器至少啟用一次字幕的工作階段數。
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
source-wordcount: '176'
ht-degree: 8%
---

# 受隱藏式字幕影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受隱藏式字幕影響的&#x200B;**資料流**報告量度。 請參閱[隱藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

受隱藏式字幕影響的&#x200B;**資料流**&#x200B;量度會計入檢視器至少啟用一次字幕的工作階段。 量度是工作階段層級的布林值；在相同工作階段中，多個註解會與一個受影響的資料流切換。 若要取得啟用字幕的磁碟區總數，請使用[隱藏式字幕計數](closed-captioning-count.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到註解啟用狀態開始事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.closedcaptioning.set`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "closedCaptioning"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
