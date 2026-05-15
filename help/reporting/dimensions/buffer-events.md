---
title: 緩衝事件（維度）
description: 報告每個工作階段的緩衝事件計數。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# 緩衝事件（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**緩衝事件**維度。 Adobe Analytics會從相同的`a.media.qoe.bufferCount`內容資料變數自動填入配對的[緩衝事件（量度）](/help/reporting/metrics/buffer-events.md)。 Customer Journey Analytics公開單一`mediaReporting.qoeDataDetails.bufferCount`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**緩衝事件**&#x200B;維度會報告工作階段期間發生的緩衝事件計數。 使用維度，以依據確切的緩衝計數來劃分參與。

## 如何填入此維度

媒體後端會在播放器每次進入`buffer`狀態時遞增計數。 此值會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bufferCount`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## 維度項目

每個專案都是關閉呼叫時所回報的常值緩衝計數值。 對於工作階段層級的布林值報告（工作階段是否遇到任何緩衝），請使用[緩衝影響的資料流](/help/reporting/metrics/buffer-impacted-streams.md)。
