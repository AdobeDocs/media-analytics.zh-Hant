---
title: 章節計數
description: 報告在工作階段期間開始的章節數量。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# 章節計數

**章節計數**&#x200B;量度會報告工作階段期間開始的章節數量。 用它來比較不同內容的章節使用情況。 對於依章節維度（章節名稱、位置）樞紐分析的章節開始計數，請使用啟用Chapters變數類別時可用的Chapter starts量度。

## 此量度的計算方式

在工作階段期間每收到[章節開始](/help/implementation/events/chapters/chapter-start.md)事件，媒體後端就會遞增`mediaReporting.sessionDetails.chapterCount`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.chapterCount`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.chapterCount`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
