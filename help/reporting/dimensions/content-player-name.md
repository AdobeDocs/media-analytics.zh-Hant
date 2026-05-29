---
title: 內容播放器名稱
description: 報告哪些播放器呈現每個媒體工作階段。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---


# 內容播放器名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容播放器名稱**&#x200B;報告維度。 如需如何收集此變數，請參閱[內容播放器名稱](/help/implementation/variables/core/content-player-name.md)。*

>[!ENDSHADEBOX]

**內容播放器名稱**&#x200B;維度會報告哪個播放器轉譯了每個媒體工作階段（例如，`HTML5 Player`、`Brightcove`或`Roku Player`）。 用它來比較相同屬性中不同玩家的參與度、完成度和品質。

## 如何填入此維度

播放器名稱由播放器在工作階段開始時設定，並持續存在於工作階段期間。 值會在每個事件時傳送，並在Adobe Analytics和Customer Journey Analytics中回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.playerName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>如果未設定播放器名稱，則會針對該工作階段取消填入維度。 報表中無法以播放器來劃分沒有播放器名稱的工作階段。

## 維度項目

每個專案都是工作階段開始時設定的常值字串。 對每個播放器使用穩定、不同的名稱，以便不同播放器的資料不會摺疊成單一條列專案。
