---
title: 發行者
description: 報告音訊內容發佈者。
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
source-wordcount: '114'
ht-degree: 12%
---

# 發行者

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**發佈者**&#x200B;報告維度。 請參閱[Publisher](/help/implementation/variables/standard-metadata/publisher.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**發佈者**&#x200B;維度會報告音訊內容發佈者（例如，播客網路或有聲書發佈者）。 用它來比較已組織之音訊目錄中不同發佈者的參與情形。

## 如何填入此維度

Publisher是在工作階段開始時，由播放器針對音訊內容所設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.publisher`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## 維度項目

每個專案都是工作階段開始時所回報的常值發佈者名稱。
