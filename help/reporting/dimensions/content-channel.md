---
title: 內容管道
description: 報告每個工作階段播放所在的分發站台、網路或屬性。
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
source-wordcount: '163'
ht-degree: 8%
---

# 內容管道

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容管道**報告維度。 如需如何收集此變數，請參閱[內容管道](/help/implementation/variables/core/content-channel.md)。*

>[!ENDSHADEBOX]

**內容管道**&#x200B;維度會報告每個工作階段播放所在的分發站、網路或屬性。 用它來中斷依網路或屬性區段的播放。

## 如何填入此維度

頻道由播放器在工作階段開始時設定，並持續存在於工作階段期間。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.channel`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>如果管道未設定，則會為該工作階段取消填入維度。

## 維度項目

每個專案都是工作階段開始時設定的常值字串。 可接受任何字串。 典型值是網路名稱、網站路徑的一部分或內部屬性識別碼。
