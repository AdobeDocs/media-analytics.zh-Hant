---
title: MVPD
description: 報告使用者驗證的纜線、衛星或虛擬提供者。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 9%

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
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.pass.mvpd`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## 維度項目

每個專案都是工作階段開始時回報的常值MVPD名稱。 使用每個提供者的規範Adobe Pass MVPD識別碼，讓資料上滾至每個提供者的單一條列專案。
