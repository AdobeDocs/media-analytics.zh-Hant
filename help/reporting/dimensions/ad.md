---
title: 廣告
description: 報告每個播放的唯一廣告，並以廣告ID作為金鑰。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# 廣告

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告**報告維度。 請參閱[廣告ID](/help/implementation/variables/ads/ad-id.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**廣告**&#x200B;維度會報告每個播放的唯一廣告，並以[廣告開始](/help/implementation/events/ads/ad-start.md)上設定的廣告ID作為索引鍵。 此維度是廣告報告的主要劃分，以及廣告名稱、廣告長度和Creative ID等廣告層級分類的聯結索引鍵。

## 如何填入此維度

廣告由播放器在每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件上設定為廣告的穩定識別碼。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.name`收集。 持續存在於造訪期間。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>廣告ID為必要項。 如果取消設定或空白，則會從串流媒體廣告報表中捨棄廣告。

## 維度項目

每個專案都是在[廣告開始](/help/implementation/events/ads/ad-start.md)報告的唯一廣告ID。 對每個創意內容使用穩定識別碼，以便相同廣告跨工作階段彙總為單一條列專案。
