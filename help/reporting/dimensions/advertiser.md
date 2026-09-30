---
title: 廣告商
description: 報告每個廣告中所精選的公司或品牌。
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
source-wordcount: '117'
ht-degree: 13%
---

# 廣告商

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告商**&#x200B;報告維度。 請參閱[廣告商](/help/implementation/variables/ads/advertiser.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**廣告商**&#x200B;維度會報告每個廣告中精選的公司或品牌（例如，`"Ford"`或`"Coca-Cola"`）。 使用維度可劃分廣告商的參與和完成。

## 如何填入此維度

廣告商由播放器於每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.ad.advertiser`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## 維度項目

每個專案都是在[廣告開始](/help/implementation/events/ads/ad-start.md)報告的常值廣告商名稱。
