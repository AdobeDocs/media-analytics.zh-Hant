---
title: 已驗證
description: 計算使用者已透過Adobe Pass獲得授權的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---


# 已驗證

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**已授權**&#x200B;報告量度。 請參閱[Authorized](/help/implementation/variables/standard-metadata/authorized.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Authorized**&#x200B;量度會計入使用者已透過Adobe Pass或TV-Everywhere獲得授權的工作階段。 與[MVPD](/help/reporting/dimensions/mvpd.md)維度配對，以中斷提供者的驗證磁碟區。

## 此量度的計算方式

當播放器在工作階段開始時將該工作階段標示為已授權時，媒體後端會增加計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.pass.auth`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
