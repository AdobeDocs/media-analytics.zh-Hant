---
title: 廣告播放器名稱
description: 報告哪個播放器演算了每個廣告。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 10%
---

# 廣告播放器名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告播放器名稱**報告維度。 如需如何收集此變數，請參閱[廣告播放器名稱](/help/implementation/variables/ads/ad-player-name.md)。*

>[!ENDSHADEBOX]

**廣告播放器名稱**&#x200B;維度會報告哪個播放器轉譯了每個廣告（例如，`"Freewheel"`、`"Google IMA"`）。 伺服器端廣告插入服務連結廣告時，廣告播放器可能會與主要內容播放器不同。

## 如何填入此維度

廣告播放器名稱是由播放器在每個[廣告開始](/help/implementation/events/ads/ad-start.md)事件上設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.ad.playerName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料饋送 | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## 維度項目

每個專案都是在[廣告開始](/help/implementation/events/ads/ad-start.md)上回報的常值廣告播放器名稱。
