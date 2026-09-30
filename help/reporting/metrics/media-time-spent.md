---
title: 媒體逗留時間
description: 報告每個工作階段作用中播放的總秒數，包括廣告。
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
source-wordcount: '182'
ht-degree: 8%
---

# 媒體逗留時間

**媒體逗留時間**&#x200B;量度會報告每個工作階段作用中播放的總秒數，包括主要內容和廣告，但不包括暫停、緩衝和停頓。 用它來測量檢視器與播放器互動的總時間。 僅針對主要內容，使用[內容逗留時間](content-time-spent.md)。

## 此量度的計算方式

在主要內容或廣告上，媒體後端會加總播放器處於`play`狀態時事件之間經過的時鐘時間。 暫停期間、緩衝事件和停止的時間會被排除。 量度會在關閉呼叫時回報。 值在Analysis Workspace中顯示為`HH:MM:SS`，在資料摘要、Data Warehouse及報表API中以秒為單位顯示。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.totalTimePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
