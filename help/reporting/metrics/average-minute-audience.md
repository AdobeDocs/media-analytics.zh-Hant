---
title: 平均分鐘觀眾數
description: 報告內容執行階段中任何指定分鐘觀看的平均檢視者數量。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# 平均分鐘觀眾數

**平均每分鐘觀眾數**&#x200B;量度會報告內容執行階段中任何指定分鐘觀看的平均檢視者人數。 這是標準的「AMA」測量，用來比較不同長度內容間的媒體觸及率。

## 此量度的計算方式

媒體後端會將每個工作階段的平均每分鐘觀眾數計算為`Content time spent / Content length`。 跨工作階段加總後，總計表示內容每分鐘的平均對象人數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.averageMinuteAudience`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>平均每分鐘觀眾數需要非零的[內容長度](/help/reporting/dimensions/content-length.md)。 如果內容長度未設定或為零，則不會為工作階段產生此量度。
