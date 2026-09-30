---
title: 總延遲期間
description: 報告跨工作階段之總和平均的累計延遲時間。
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
source-wordcount: '210'
ht-degree: 7%
---

# 總延遲期間

**總停頓期間**&#x200B;量度會報告跨工作階段的累積停頓時間，適用於總計、平均值和百分位數統計。 使用量度可計算檢視者在報表時段內等候已逾期的播放所花費的總時間。

在Customer Journey Analytics中，`xdm.mediaReporting.qoeDataDetails.stallTime`可作為量度或維度使用，而不需要個別的維度元件。

## 此量度的計算方式

媒體後端會加總每個停頓間隔的持續時間，當主要內容上至少有三個連續事件未記錄播放點移動時偵測到。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.qoe.stallTime`對應至自訂事件的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`，`post_event_list` （處理規則將`a.media.qoe.stallTime`對應至的自訂事件；請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
