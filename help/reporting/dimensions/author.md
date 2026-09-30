---
title: 作者
description: 報告內容的作者。 主要用於有聲書。
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
source-wordcount: '119'
ht-degree: 11%
---

# 作者

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**作者**報告維度。 請參閱[作者](/help/implementation/variables/standard-metadata/author.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**作者**&#x200B;維度會報告內容的作者（例如，`"Eleanor Clementine"`）。 主要用於有聲書，但也適用於其主機或製作者是相關歸因的播客。

## 如何填入此維度

作者是在工作階段開始時，由播放器針對音訊內容所設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.author`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## 維度項目

每個專案都是工作階段開始時所回報的常值作者名稱。
