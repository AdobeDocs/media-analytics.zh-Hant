---
title: 位元速率變更（維度）
description: 報告每個工作階段的位元速率變更事件計數。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# 位元速率變更（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**位元速率變更**維度。 Adobe Analytics會從相同的`a.media.qoe.bitrateChangeCount`內容資料變數自動填入配對的[位元速率變更（量度）](/help/reporting/metrics/bitrate-changes.md)。 Customer Journey Analytics公開單一`mediaReporting.qoeDataDetails.bitrateChangeCount`欄位，您可將其作為維度或量度使用。 請參閱[位元速率變更](/help/implementation/variables/quality/bitrate-change.md)，瞭解如何引發位元速率變更事件。*

>[!ENDSHADEBOX]

**位元速率變更**&#x200B;維度會報告工作階段期間發生的位元速率變更事件計數。 使用維度，以精確的變更計數值來劃分參與度和品質（例如「有3個位元速率變更的工作階段與有0的工作階段」）。

## 如何填入此維度

媒體後端會遞增工作階段期間每收到[位元速率變更](/help/implementation/events/playback/bitrate-change.md)事件的計數。 此值會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bitrateChangeCount`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## 維度項目

每個專案都是關閉呼叫時回報的常值變更計數值。 對於工作階段層級的布林值報告（工作階段是否經歷任何位元速率變更），請使用[位元速率變更影響的資料流](/help/reporting/metrics/bitrate-change-impacted-streams.md)。
