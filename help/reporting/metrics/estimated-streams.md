---
title: 預估資料流
description: 約略每個工作階段的音訊或視訊資料流的數量。
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
source-wordcount: '190'
ht-degree: 10%
---

# 預估資料流

**預估資料流**&#x200B;量度約等於每個工作階段的音訊或視訊資料流數量，每30分鐘播放一次就會計算一個資料流。 此版本旨在達成內容整合合約，並達成近似效果，讓每個30分鐘的使用量區塊都計為單獨的「資料流」。

## 此量度的計算方式

媒體後端將此量度計算為`FLOOR(totalTimePlayed / 1800) + 1`，其中`totalTimePlayed`是[媒體逗留時間](media-time-spent.md)秒。 量度會在關閉呼叫時回報。

| 媒體逗留時間 | 預估資料流 |
| --- | --- |
| 0-29分鐘 | 1 |
| 30-59分鐘 | 2 |
| 60-89分鐘 | 3 |
| 90分鐘以上 | 4+ |

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.estimatedStreams`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.estimatedStreams`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
