---
title: 廣告計數
description: 報告工作階段開始的廣告數量。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 9%

---


# 廣告計數

**廣告計數**&#x200B;量度會報告工作階段期間開始的廣告數量。 用它來瞭解依內容、頻道或資料流型別的廣告載入。 對於由廣告維度（廣告商、行銷活動、創意）樞紐分析的廣告開始計數，請使用啟用廣告變數類別時可用的廣告開始量度。

## 此量度的計算方式

媒體後端會在工作階段期間每收到[廣告開始](/help/implementation/events/ads/ad-start.md)事件時遞增此計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.adCount`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.adCount`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
