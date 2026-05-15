---
title: 作者
description: 報告內容的作者。 主要用於有聲書。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
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
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.author`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## 維度項目

每個專案都是工作階段開始時所回報的常值作者名稱。
