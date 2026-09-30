---
title: 內容名稱
description: 報告每個媒體工作階段的人類可讀標題。
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
source-wordcount: '162'
ht-degree: 11%
---

# 內容名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容名稱**報告維度。 如需如何收集此變數，請參閱[內容名稱](/help/implementation/variables/core/content-name.md)。*

>[!ENDSHADEBOX]

**內容名稱**&#x200B;維度會報告每個媒體工作階段的人類可讀標題。

## 如何填入此維度

易記名稱由播放器在工作階段開始時設定。 報告的值與傳送的內容相符。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.friendlyName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>在Adobe Analytics中，此值也對應至[Content](content.md)維度上的&#x200B;**影片名稱**&#x200B;分類。 您需個別負責填入及維護該分類。 Customer Journey Analytics直接使用此維度。

>[!IMPORTANT]
>
>如果未設定內容名稱，則會針對該工作階段取消填入維度。

## 維度項目

每個專案都是工作階段開始時報告的常值標題（例如，`"Blinding Light"`）。
