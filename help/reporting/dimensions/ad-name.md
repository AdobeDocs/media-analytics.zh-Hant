---
title: 廣告名稱
description: 報告每個廣告的人類可讀標題。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# 廣告名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告名稱**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告名稱](/help/implementation/variables/ads/ad-name.md)。*

>[!ENDSHADEBOX]

**廣告名稱**&#x200B;維度會報告每個廣告的人類可讀標題。

## 如何填入此維度

廣告名稱由播放器在每個`media.adStart`事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.friendlyName`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadname, post_videoadname` |

在Adobe Analytics中，此維度會以兩種方式顯示：作為&#x200B;**廣告名稱（變數）** （直接從`a.media.ad.friendlyName`收集）以及作為&#x200B;**廣告名稱** （衍生自[廣告](ad.md)維度的分類）。 如果您使用分類，則需負責使用[分類集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護其值。 使用&#x200B;**廣告名稱（變數）**&#x200B;不需要分類維護，但您會失去廣告名稱與上層[廣告](ad.md)維度之間保證的1:1關係。 使用實作工作流程最支援的元件。

## 維度項目

每個專案都是`media.adStart`上報告的常值廣告標題（例如，`"Ford F-150"`）。
