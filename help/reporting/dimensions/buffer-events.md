---
title: 緩衝事件（維度）
description: 報告每個工作階段的緩衝事件計數。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 8%
---

# 緩衝事件（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**緩衝事件**維度。 Adobe Analytics會從相同的`a.media.qoe.bufferCount`內容資料變數自動填入配對的[緩衝事件（量度）](/help/reporting/metrics/buffer-events.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.bufferCount`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**緩衝事件**&#x200B;維度會報告工作階段期間發生的緩衝事件計數。 使用維度，以依據確切的緩衝計數來劃分參與。

## 如何填入此維度

媒體後端會在播放器每次進入`buffer`狀態時遞增計數。 此值會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.bufferCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## 維度項目

每個專案都是關閉呼叫時所回報的常值緩衝計數值。 對於工作階段層級的布林值報告（工作階段是否遇到任何緩衝），請使用[緩衝影響的資料流](/help/reporting/metrics/buffer-impacted-streams.md)。
