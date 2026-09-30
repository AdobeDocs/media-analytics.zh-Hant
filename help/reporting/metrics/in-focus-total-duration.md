---
title: 觀看中總時間
description: 報告播放器在工作階段期間觀看中的累積秒數。
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
source-wordcount: '177'
ht-degree: 8%
---

# 觀看中總時間

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**觀看中總時間**&#x200B;報告量度。 請參閱[焦點](/help/implementation/variables/player-state/in-focus.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**觀看中總時間**&#x200B;量度會報告播放器在工作階段期間觀看中的累計時間（以秒為單位）。 後端會加總焦點狀態 — 開始與相符狀態 — 結束事件之間的每個間隔。

## 此量度的計算方式

工作階段期間所有觀看中間隔的媒體後端經過時間總和。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.infocus.time`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "inFocus"`，欄位`time` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
