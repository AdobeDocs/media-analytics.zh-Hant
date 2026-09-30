---
title: 章節開始
description: 計算工作階段期間開始播放的每個章節。
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
source-wordcount: '116'
ht-degree: 12%
---

# 章節開始

**章節開始**&#x200B;量度會計算工作階段期間開始播放的每個章節。 將其與[章節完成](chapter-completes.md)配對，以計算章節完成率。

## 此量度的計算方式

當收到[章節開始](/help/implementation/events/chapters/chapter-start.md)事件時，媒體後端會設定此旗標。 量度會在章節關閉呼叫上報告。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體章節]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.chapter.view`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
