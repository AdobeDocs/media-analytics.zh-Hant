---
title: 媒體摘要型別
description: 透過多個摘要提供相同內容時，會報告廣播摘要（例如East-HD或West-SD）。
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

# 媒體摘要型別

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**媒體摘要型別**報告維度。 如需如何收集此變數，請參閱[媒體摘要型別](/help/implementation/variables/standard-metadata/media-feed-type.md)。*

>[!ENDSHADEBOX]

**媒體摘要型別**&#x200B;維度會報告每個工作階段的廣播摘要（例如，`"East-HD"`、`"West-SD"`或`"4K"`）。 當透過多個區域或品質摘要提供相同內容，且每個摘要需要報告參與時，請使用它。

## 如何填入此維度

媒體摘要型別是由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.feed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## 維度項目

每個專案是在工作階段開始時報告的常值摘要值。 根據地區或品質分割使用一組穩定的摘要識別碼。
