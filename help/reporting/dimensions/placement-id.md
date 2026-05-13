---
title: 版面 ID
description: 報告每個廣告的位置識別碼。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# 版面 ID

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**位置ID**報告維度。 如需如何收集此變數，請參閱[位置ID](/help/implementation/variables/ads/placement-id.md)。*

>[!ENDSHADEBOX]

**位置ID**&#x200B;維度會報告廣告位置識別碼（通常是廣告伺服器平台中定義的位置或區域）。 使用維度來比較不同位置位置的參與度和完成度。

## 如何填入此維度

播放器會在每個`media.adStart`事件上設定位置ID。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.ad.placement`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.placement`對應至的eVar） |

## 維度項目

每個專案都是`media.adStart`上報告的常值位置值。
