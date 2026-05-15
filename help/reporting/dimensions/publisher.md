---
title: 發行者
description: 報告音訊內容發佈者。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 發行者

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**發佈者**報告維度。 請參閱[Publisher](/help/implementation/variables/standard-metadata/publisher.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**發佈者**&#x200B;維度會報告音訊內容發佈者（例如，播客網路或有聲書發佈者）。 用它來比較已組織之音訊目錄中不同發佈者的參與情形。

## 如何填入此維度

Publisher是在工作階段開始時，由播放器針對音訊內容所設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.publisher`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## 維度項目

每個專案都是工作階段開始時所回報的常值發佈者名稱。
