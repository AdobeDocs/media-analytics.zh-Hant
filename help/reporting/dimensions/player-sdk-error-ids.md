---
title: 播放器SDK錯誤ID
description: 報告內容播放器SDK產生的唯一錯誤識別碼。
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
source-wordcount: '159'
ht-degree: 8%
---

# 播放器SDK錯誤ID

**播放器SDK錯誤ID**&#x200B;維度會報告內容播放器SDK在工作階段期間產生的唯一錯誤識別碼。 播放器必須透過錯誤追蹤API，在實施時提供程式碼或ID。 支援每個工作階段有多個錯誤ID。

## 如何填入此維度

播放器會將播放器 — SDK錯誤ID傳遞至[錯誤](/help/implementation/events/error.md)事件的追蹤器。 後端會收集工作階段中的唯一ID，並在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.playerSdkErrors`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## 維度項目

每個專案都是播放器SDK產生的錯誤代碼或ID。 跨實施使用穩定分類法，以便錯誤ID可跨工作階段正確彙總。
