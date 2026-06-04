---
title: 節目
description: 報告屬於某個系列之視訊內容的節目或系列名稱。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# 節目

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**節目**&#x200B;報告維度。 請參閱[節目](/help/implementation/variables/standard-metadata/show.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Show**&#x200B;維度會報告節目或系列名稱。 多季的集數會統計為相同的節目條列專案，因此請使用它來比較整個系列期限的參與度。

## 如何填入此維度

當內容屬於一系列內容時，播放器會在工作階段開始時設定節目。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.show`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## 維度項目

每個專案都是工作階段開始時報告的常值顯示名稱（例如，`"Blinding Light"`）。 每次顯示使用穩定、不同的名稱，資料就不會在共用一個字的非相關程式中摺疊。
