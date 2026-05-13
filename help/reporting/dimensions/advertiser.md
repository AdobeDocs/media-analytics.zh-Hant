---
title: 廣告商
description: 報告每個廣告中所精選的公司或品牌。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# 廣告商

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告商**&#x200B;報告維度。 請參閱[廣告商](/help/implementation/variables/ads/advertiser.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**廣告商**&#x200B;維度會報告每個廣告中精選的公司或品牌（例如，`"Ford"`或`"Coca-Cola"`）。 使用維度可劃分廣告商的參與和完成。

## 如何填入此維度

廣告商由播放器於每個`media.adStart`事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.advertiser`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadvertiser, post_videoadvertiser` |

## 維度項目

每個專案都是`media.adStart`上報告的常值廣告商名稱。
