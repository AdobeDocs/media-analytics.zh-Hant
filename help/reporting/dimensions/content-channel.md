---
title: 內容管道
description: 報告每個工作階段播放所在的分發站台、網路或屬性。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 6%

---


# 內容管道

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容管道**報告維度。 如需如何收集此變數，請參閱[內容管道](/help/implementation/variables/core/content-channel.md)。*

>[!ENDSHADEBOX]

**內容管道**&#x200B;維度會報告每個工作階段播放所在的分發站、網路或屬性。 用它來中斷依網路或屬性區段的播放。

## 如何填入此維度

頻道由播放器在工作階段開始時設定，並持續存在於工作階段期間。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.channel`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videochannel, post_videochannel` |

>[!IMPORTANT]
>
>如果管道未設定，則會為該工作階段取消填入維度。

## 維度項目

每個專案都是工作階段開始時設定的常值字串。 可接受任何字串。 典型值是網路名稱、網站路徑的一部分或內部屬性識別碼。
