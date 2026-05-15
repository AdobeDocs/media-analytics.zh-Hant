---
title: 廣告播放器名稱
description: 報告哪個播放器演算了每個廣告。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# 廣告播放器名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告播放器名稱**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告播放器名稱](/help/implementation/variables/ads/ad-player-name.md)。*

>[!ENDSHADEBOX]

**廣告播放器名稱**&#x200B;維度會報告哪個播放器轉譯了每個廣告（例如，`"Freewheel"`、`"Google IMA"`）。 伺服器端廣告插入服務連結廣告時，廣告播放器可能會與主要內容播放器不同。

## 如何填入此維度

廣告播放器名稱是由播放器在每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.playerName`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## 維度項目

每個專案都是在[廣告開始](/help/implementation/events/ads/ad-start.md)上回報的常值廣告播放器名稱。
