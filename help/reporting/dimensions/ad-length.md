---
title: 廣告長度
description: 報告每個廣告的持續時間（以秒為單位）。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# 廣告長度

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告長度**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告長度](/help/implementation/variables/ads/ad-length.md)。*

>[!ENDSHADEBOX]

**廣告長度**&#x200B;維度會報告每個廣告的持續時間（秒）。

## 如何填入此維度

廣告長度是由播放器於每個`media.adStart`事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.length`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadlength, post_videoadlength` |

在Adobe Analytics中，此維度會以兩種方式顯示：作為&#x200B;**廣告長度（變數）** （直接從`a.media.ad.length`收集）以及作為&#x200B;**廣告長度** （衍生自[廣告](ad.md)維度的分類）。 如果您使用分類，則需負責使用[分類集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護其值。 使用&#x200B;**廣告長度（變數）**&#x200B;不需要分類維護，但您會失去廣告長度和上層[廣告](ad.md)維度之間保證的1:1關係。 使用實作工作流程最支援的元件。

## 維度項目

每個專案都是在`media.adStart`上報告的常值廣告長度值（以秒為單位）。
