---
title: 外部錯誤ID
description: 報告來自外部來源的唯一錯誤識別碼，例如CDN錯誤。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# 外部錯誤ID

**外部錯誤ID**&#x200B;維度會報告來自播放器SDK外部之任何來源的唯一錯誤識別碼（例如CDN錯誤）。 播放器必須透過錯誤追蹤API，在實施時提供程式碼或ID。 支援每個工作階段有多個錯誤ID。

## 如何填入此維度

播放器會將外部錯誤ID傳遞至`media.error`事件的追蹤器。 後端會收集工作階段中的唯一ID，並在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.externalErrors`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoeextneralerrors` |

## 維度項目

每個專案都是播放器提供的錯誤代碼或ID。 跨實施使用穩定分類法，以便錯誤ID可跨工作階段正確彙總。
