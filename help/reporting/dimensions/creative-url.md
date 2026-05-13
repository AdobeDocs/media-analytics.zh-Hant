---
title: 創作 URL
description: 報告每個廣告創意的資產URL。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 9%

---


# 創作 URL

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**Creative URL**&#x200B;報告維度。 如需如何收集此變數，請參閱[Creative URL](/help/implementation/variables/ads/creative-url.md)。*

>[!ENDSHADEBOX]

**Creative URL**&#x200B;維度會報告每個廣告創意的資產URL。 當URL本身對分析有意義時（例如，區分CDN路徑或創意版本），請使用維度。

## 如何填入此維度

Creative URL是由播放器在每個`media.adStart`事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.ad.creativeURL`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.creativeURL`對應至的eVar） |

## 維度項目

每個專案都是`media.adStart`上報告的常值URL字串。
