---
title: 集數
description: 報告一個季節內的集數。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---


# 集數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**集數**報告維度。 請參閱[Episode](/help/implementation/variables/standard-metadata/episode.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Episode**&#x200B;維度會報告一季中的集數。 與[節目](show.md)和[季](season.md)搭配使用，以便在個別集數層級中斷參與。

## 如何填入此維度

集數由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.episode`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## 維度項目

每個專案都是工作階段開始時報告的常值集值（通常是字串整數，例如`"13"`）。 單是集數在跨季時並不唯一；與季配對，可取得明確的分組結果。
