---
title: 集數
description: 報告一個季節內的集數。
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
source-wordcount: '132'
ht-degree: 12%
---

# 集數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**集數**&#x200B;報告維度。 請參閱[Episode](/help/implementation/variables/standard-metadata/episode.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Episode**&#x200B;維度會報告一季中的集數。 與[節目](show.md)和[季](season.md)搭配使用，以便在個別集數層級中斷參與。

## 如何填入此維度

集數由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.episode`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## 維度項目

每個專案都是工作階段開始時報告的常值集值（通常是字串整數，例如`"13"`）。 單是集數在跨季時並不唯一；與季配對，可取得明確的分組結果。
