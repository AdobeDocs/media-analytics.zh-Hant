---
title: MVPD
description: 報告使用者驗證的纜線、衛星或虛擬提供者。
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
source-wordcount: '150'
ht-degree: 10%
---

# MVPD

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**MVPD**&#x200B;報告維度。 請參閱[MVPD](/help/implementation/variables/standard-metadata/mvpd.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**MVPD** （多頻道視訊節目經銷商）維度會報告提供者，使用者透過該提供者透過Adobe Pass進行驗證（例如，`"Comcast"`或`"DirecTV"`）。 用它來中斷驗證提供者的參與。

## 如何填入此維度

MVPD是由播放器在工作階段開始時，在內容被封鎖在Adobe Pass之後時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.pass.mvpd`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## 維度項目

每個專案都是工作階段開始時回報的常值MVPD名稱。 使用每個提供者的規範Adobe Pass MVPD識別碼，讓資料上滾至每個提供者的單一條列專案。
