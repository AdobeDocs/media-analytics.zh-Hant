---
title: 開始時間（量度）
description: 報告跨工作階段之總和平均值的啟動時間。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---


# 開始時間（量度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**開始時間**&#x200B;量度。 Adobe Analytics會從相同的`a.media.qoe.timeToStart`內容資料變數自動填入配對的[開始時間（維度）](/help/reporting/dimensions/time-to-start.md)。 Customer Journey Analytics公開單一`mediaReporting.qoeDataDetails.timeToStart`欄位，您可將其作為維度或量度使用。 如需如何收集此變數，請參閱[開始時間](/help/implementation/variables/quality/time-to-start.md)。*

>[!ENDSHADEBOX]

**開始時間**&#x200B;量度會報告跨工作階段的啟動時間，適用於總和、平均值及百分位數統計。 使用量度可計算報告期間內的平均啟動時間，並比較不同內容、網路或播放器的啟動效能。 Adobe會以秒為單位儲存值，並在擷取時從播放器報表轉換毫秒。

## 此量度的計算方式

在工作階段開始引發之前，播放器會設定QoE物件上的`timeToStart`。 後端會報告關閉呼叫的值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.timeToStart`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
