---
title: 掉格（量度）
description: 報告跨工作階段之總和平均值的累計掉格。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# 掉格（量度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**掉格**量度。 Adobe Analytics會從相同的`a.media.qoe.droppedFrameCount`內容資料變數自動填入配對的[掉格（維度）](/help/reporting/dimensions/dropped-frames.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.droppedFrames`欄位，您可將其作為維度或量度使用。 如需如何收集此變數，請參閱[掉格](/help/implementation/variables/quality/dropped-frames.md)。*

>[!ENDSHADEBOX]

**掉格**&#x200B;量度會報告跨工作階段的累積掉格，適用於總和、平均值及百分位數統計。 使用量度可計算報告期間的總下拉量，並比較不同內容、網路或播放器之間的框架轉譯品質。

## 此量度的計算方式

播放器會將QoE物件的`droppedFrames`值更新為遞減累積。 後端會報告關閉呼叫的最新值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.droppedFrameCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

對於工作階段層級的布林報表（無論是否有任何影格被卸除），請使用[受影響的](dropped-frame-impacted-streams.md)個卸除影格。
