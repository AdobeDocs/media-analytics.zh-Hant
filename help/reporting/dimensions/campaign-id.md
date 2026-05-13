---
title: 行銷活動 ID
description: 報告每個廣告所屬的行銷活動。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 行銷活動 ID

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**促銷活動識別碼**報告維度。 如需如何收集此變數，請參閱[促銷活動識別碼](/help/implementation/variables/ads/campaign-id.md)。*

>[!ENDSHADEBOX]

**行銷活動ID**&#x200B;維度會報告每個廣告創意所屬的廣告行銷活動。 使用維度，可在共用行銷活動的多個創意人員之間彙總參與度。

## 如何填入此維度

行銷活動ID是由播放器在每個`media.adStart`事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.campaign`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videocampaign, post_videocampaign` |

## 維度項目

每個專案都是在`media.adStart`上報告的常值行銷活動值。
