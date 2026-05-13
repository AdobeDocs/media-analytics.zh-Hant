---
title: 平均位元速率（量度）
description: 報告每個工作階段的原始加權平均位元速率（以每秒位元組數為單位）。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 7%

---


# 平均位元速率（量度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**平均位元速率**&#x200B;事件量度，此量度會報告每個工作階段的原始加權平均位元速率。 請參閱分段維度的平均位元速率（維度）[&#128279;](/help/reporting/dimensions/average-bitrate.md)。 如需如何收集此變數，請參閱[位元速率](/help/implementation/variables/quality/bitrate.md)。*

>[!ENDSHADEBOX]

**平均位元速率**&#x200B;量度會報告每個工作階段的原始加權平均播放位元速率（以kbps為單位）。 與[分段維度](/help/reporting/dimensions/average-bitrate.md)不同，量度是連續數值，適用於跨工作階段的加總、平均和百分位數統計。

## 此量度的計算方式

媒體後端會計算工作階段期間報告的所有位元速率值的加權平均值，加權依據是每個位元速率作用中的持續時間。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bitrateAverage`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
