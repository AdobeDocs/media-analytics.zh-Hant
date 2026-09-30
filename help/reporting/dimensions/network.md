---
title: 網路
description: 報告廣播網路或頻道名稱。
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
source-wordcount: '127'
ht-degree: 12%
---

# 網路

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**網路**&#x200B;報告維度。 請參閱[網路](/help/implementation/variables/standard-metadata/network.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**網路**&#x200B;維度會報告廣播網路或頻道名稱（例如，`"Fox"`或`"ESPN"`）。 使用它來比較相同串流屬性內跨網路的參與度。

## 如何填入此維度

網路是在工作階段開始時由播放器設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.network`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## 維度項目

每個專案都是工作階段開始時報告的常值網路值。 針對每個網路使用穩定、不同的名稱，以免資料在拼字變異之間產生片段。
