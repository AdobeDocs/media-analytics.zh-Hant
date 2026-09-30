---
title: 藝術家
description: 針對音訊內容報告表演藝人。
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
source-wordcount: '128'
ht-degree: 10%
---

# 藝術家

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**藝人**&#x200B;報告維度。 請參閱[藝人](/help/implementation/variables/standard-metadata/artist.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**藝人**&#x200B;維度會報告音訊內容的演出藝人（例如，`"Crested Larks"`）。 用它來打破表演者在音樂或播客目錄上的參與。

## 如何填入此維度

藝人是在工作階段開始時，由播放器針對音訊內容所設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.artist`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## 維度項目

每個專案都是工作階段開始時所回報的藝術家常值名稱。 使用每個藝人的穩定正式名稱，讓資料不會跨格式變體而分段。
