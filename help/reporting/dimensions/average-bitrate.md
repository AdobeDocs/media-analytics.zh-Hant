---
title: 平均位元速率（維度）
description: 以100 kbps的間隔報告每個工作階段的分段平均位元速率。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# 平均位元速率（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**平均位元速率**&#x200B;維度，此維度會報告每個工作階段的分段位元速率。 請參閱原始加權平均量度的[平均位元速率（量度）](/help/reporting/metrics/average-bitrate.md)。 如需如何收集此變數，請參閱[位元速率](/help/implementation/variables/quality/bitrate.md)。*

>[!ENDSHADEBOX]

**平均位元速率**&#x200B;維度會報告每個工作階段的平均播放位元速率（以100 kbps間隔分組）。 後端會將值計算為工作階段中所有位元速率值的加權平均值，然後將其指派給貯體。 使用維度可依位元速率層級劃分參與度和品質。

## 如何填入此維度

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bitrateAverageBucket`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebitrateaverageevar, post_videoqoebitrateaverageevar` |

## 維度項目

每個專案都是位元貯體標籤（例如，`800-899`、`3200-3299`）。 將[平均位元速率（量度）](/help/reporting/metrics/average-bitrate.md)用於原始加權平均值，而不是分段維度。
