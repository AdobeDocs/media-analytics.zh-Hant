---
title: 計算量度
description: Adobe Analytics和Customer Journey Analytics中串流媒體報表的自訂計算量度。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 計算量度

Adobe串流媒體服務的計算量度是根據標準串流媒體量度建置的自訂量度，可讓您在不變更實施的情況下衍生出平均廣告逗留時間或媒體完成率等比率。

若要在Analysis Workspace中建立這些計算量度，請在[Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/components/calculated-metrics/cm-overview)或[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)中檢視個別計算量度概觀。

| 計算量度 | 說明 | 公式 |
| --- | --- | --- |
| 平均 每個媒體資料流的廣告 | 每個[&#128279;](/help/reporting/metrics/media-starts.md)媒體開始的[[!UICONTROL 廣告開始次數]](/help/reporting/metrics/ad-starts.md) | `[Ad starts] / [Media starts]` |
| 平均 每個媒體資料流的章節數 | 每[[!UICONTROL 個媒體開始]](/help/reporting/metrics/media-starts.md)的[[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md) | `[Chapter starts] / [Media starts]` |
| 平均 媒體逗留時間 | 每[&#128279;](/help/reporting/metrics/media-starts.md)個媒體開始的[[!UICONTROL 媒體逗留時間]](/help/reporting/metrics/media-time-spent.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| 平均 內容逗留時間 | 每個[[!UICONTROL 內容開始時間]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) [[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md) | `[Content time spent] / [Content starts]` |
| 平均 廣告逗留時間 | 每[&#128279;](/help/reporting/metrics/ad-starts.md)個廣告開始的[[!UICONTROL 廣告逗留時間]](/help/reporting/metrics/ad-time-spent.md) &#x200B; (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| 平均 章節逗留時間 | 每個[&#128279;](/help/reporting/metrics/chapter-starts.md)章節開始的[[!UICONTROL 章節逗留時間]](/help/reporting/metrics/chapter-time-spent.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| 媒體完成率 | [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md)與[[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md)的比率 | `[Content completes] / [Media starts]` |
| 內容完成率 | [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md)與[[!UICONTROL 內容開始]](/help/reporting/metrics/content-starts.md)的比率 | `[Content completes] / [Content starts]` |
| 廣告完成率 | [[!UICONTROL 廣告完成]](/help/reporting/metrics/ad-completes.md)與[[!UICONTROL 廣告開始]](/help/reporting/metrics/ad-starts.md)的比率 | `[Ad completes] / [Ad starts]` |
| 章節完成率 | [[!UICONTROL 章節完成]](/help/reporting/metrics/chapter-completes.md)與[[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md)的速率 | `[Chapter completes] / [Chapter starts]` |
| 開始前掉格率 | [[!UICONTROL 開始前掉格]](/help/reporting/metrics/drops-before-start.md)與[[!UICONTROL 媒體開始前的掉格率]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| 內容暫停期間率 | 總暫停期間[&#128279;](/help/reporting/metrics/total-pause-duration.md)與[[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Total pause duration] / [Content time spent]` |
| 內容緩衝期間率 | [[!UICONTROL 總緩衝期間]](/help/reporting/metrics/total-buffer-duration.md)與[[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Total buffer duration] / [Content time spent]` |
| 內容開始時間率 | [[!UICONTROL 開始時間]](/help/reporting/metrics/time-to-start.md)與[[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Time to start] / [Content time spent]` |
| 廣告逗留時間率 | [[!UICONTROL 廣告逗留時間]](/help/reporting/metrics/ad-time-spent.md)與[[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Ad time spent] / [Content time spent]` |

