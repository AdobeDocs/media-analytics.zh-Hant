---
title: Pod位置中的廣告
description: 報告每個廣告在其上層廣告插播中的零索引位置。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 7%

---


# Pod位置中的廣告

>[!BEGINSHADEBOX]

*此頁面涵蓋pod position **報告維度中的**&#x200B;廣告。 請參閱Pod位置[&#128279;](/help/implementation/variables/ads/ad-in-pod-position.md)中的廣告，瞭解如何收集此變數。*

>[!ENDSHADEBOX]

Pod位置&#x200B;**中的**&#x200B;廣告維度會報告其上層廣告插播中每個廣告的索引零位置。 Pod中的第一個廣告是`0`，第二個是`1`，依此類推。 使用維度可依廣告插播中的位置比較參與和完成情形。

## 如何填入此維度

Pod位置中的廣告由播放器在每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.podPosition`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## 維度項目

每個專案都是整數值位置值(`0`， `1`， `2`， ...) 於[廣告開始](/help/implementation/events/ads/ad-start.md)回報。
