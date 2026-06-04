---
title: 錯誤事件
description: 計算各個工作階段之總和平均值的錯誤事件。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# 錯誤事件

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**錯誤事件**量度。 Adobe Analytics會從相同的`a.media.qoe.errorCount`內容資料變數自動填入配對的[錯誤維度](/help/reporting/dimensions/errors.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.errorCount`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**錯誤事件**&#x200B;量度會跨工作階段計算錯誤事件，適用於總和、平均值及百分位數統計。 使用量度可計算報告時段內的總錯誤量，並比較不同內容、網路或播放器的錯誤率。

## 此量度的計算方式

媒體後端會遞增播放器回報之每個錯誤的計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.errorCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

對於工作階段層級的布林值報告（無論是否發生任何錯誤），請使用[錯誤影響的資料流](error-impacted-streams.md)。
