---
title: 平均位元速率（維度）
description: 以100 kbps的間隔報告每個工作階段的分段平均位元速率。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 8%
---

# 平均位元速率（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**平均位元速率**維度，此維度會報告每個工作階段的分段位元速率。 請參閱原始加權平均量度的[平均位元速率（量度）](/help/reporting/metrics/average-bitrate.md)。 如需如何收集此變數，請參閱[位元速率](/help/implementation/variables/quality/bitrate.md)。*

>[!ENDSHADEBOX]

**平均位元速率**&#x200B;維度會報告每個工作階段的平均播放位元速率（以100 kbps間隔分組）。 後端會將值計算為工作階段中所有位元速率值的加權平均值，然後將其指派給貯體。 使用維度可依位元速率層級劃分參與度和品質。

## 如何填入此維度

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.bitrateAverageBucket`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## 維度項目

每個專案都是位元貯體標籤（例如，`800-899`、`3200-3299`）。 將[平均位元速率（量度）](/help/reporting/metrics/average-bitrate.md)用於原始加權平均值，而不是分段維度。
