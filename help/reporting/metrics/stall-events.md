---
title: 延遲事件
description: 計算各工作階段總和平均值的延遲事件。
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
source-wordcount: '203'
ht-degree: 7%
---

# 延遲事件

**Stall事件**&#x200B;量度會計算各工作階段的延遲事件，適用於總和、平均值及百分位數統計。 使用量度可計算報告期間的總延遲量，並比較不同內容、網路或播放器的延遲穩定性。

在Customer Journey Analytics中，`xdm.mediaReporting.qoeDataDetails.stallCount`可作為量度或維度使用，而不需要個別的維度元件。

## 此量度的計算方式

每次在主要內容上未記錄播放點移動至少三個連續事件時，媒體後端都會增加計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.qoe.stallCount`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.qoe.stallCount`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

對於工作階段層級的布林值報告（無論是否發生任何停頓），請使用[停頓受影響的串流](stall-impacted-streams.md)。
