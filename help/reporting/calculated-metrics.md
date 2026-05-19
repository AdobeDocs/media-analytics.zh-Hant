---
title: 計算量度
description: Adobe Analytics和Customer Journey Analytics中串流媒體報表的自訂計算量度。
feature: Metrics
role: User, Admin
source-git-commit: ea740a32bbd5e640cd437cd8c5c4f48071a0d02c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---


# 計算量度

Adobe串流媒體服務的計算量度是根據標準串流媒體量度建置的自訂量度，可讓您在不變更實施的情況下衍生出平均廣告逗留時間或媒體完成率等比率。

若要在Analysis Workspace中建立這些計算量度，請在[Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview)或[Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)中檢視個別計算量度概觀。

| 計算量度 | 說明 | 公式 |
| --- | --- | --- |
| 平均 每個媒體資料流的廣告 | 每次媒體開始的廣告開始數 | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 每個媒體資料流的章節數 | 每次媒體開始的章節開始數 | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 媒體逗留時間 | 每次媒體開始的總逗留時間(`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 內容逗留時間 | 每次內容開始的內容逗留時間(`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 平均 廣告逗留時間 | 每次廣告開始的廣告逗留時間(`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 平均 章節逗留時間 | 每次章節開始的章節逗留時間(`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 媒體完成率 | 內容完成次數與媒體起始次數的比率 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 內容完成率 | 內容完成與內容開始的比率 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 廣告完成率 | 廣告完成與廣告開始的比率 | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 章節完成率 | 章節結束與章節開始的比率 | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 開始前掉格率 | 開始前掉格與媒體開始的比率 | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 內容暫停期間率 | 總暫停期間與內容逗留時間的比率 | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 內容緩衝期間率 | 總緩衝期間與內容逗留時間的比率 | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 內容開始時間率 | 開始時間與內容逗留時間的比率 | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 廣告逗留時間率 | 廣告逗留時間與內容逗留時間的比率 | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
