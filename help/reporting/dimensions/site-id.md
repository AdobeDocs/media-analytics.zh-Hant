---
title: 網站 ID
description: 報告每個廣告的廣告網站識別碼。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# 網站 ID

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**網站識別碼**&#x200B;報告維度。 請參閱[網站ID](/help/implementation/variables/ads/site-id.md)，瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**網站ID**&#x200B;維度會報告廣告網站識別碼（通常是來自您的廣告伺服器平台的ID）。 使用維度可劃分廣告刊登網站參與度。

## 如何填入此維度

網站識別碼是由播放器在每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.ad.site`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.site`對應至的eVar） |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## 維度項目

每個專案都是在[廣告開始](/help/implementation/events/ads/ad-start.md)報告的常值網站識別碼值。
