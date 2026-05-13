---
title: 總緩衝期間（量度）
description: 報告跨工作階段之總和平均值的累積緩衝時間。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# 總緩衝期間（量度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**總緩衝期間**&#x200B;量度。 Adobe Analytics會從相同的`a.media.qoe.bufferTime`內容資料變數自動填入配對的[總緩衝期間（維度）](/help/reporting/dimensions/total-buffer-duration.md)。 Customer Journey Analytics公開單一`mediaReporting.qoeDataDetails.bufferTime`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**總緩衝期間**&#x200B;量度會報告跨工作階段的累積緩衝時間，適用於總和、平均值及百分位數統計。 使用量度可計算客戶在報表時段中花費在緩衝區的總時間。

## 此量度的計算方式

媒體後端會加總每個緩衝間隔（從`media.bufferStart`到下一個狀態變更）的持續時間。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bufferTime`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
