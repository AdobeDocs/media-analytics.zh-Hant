---
title: 相簿
description: 報告音軌所屬的相簿。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 10%

---


# 相簿

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**相簿**&#x200B;報告維度。 請參閱[相簿](/help/implementation/variables/standard-metadata/album.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**相簿**&#x200B;維度會報告音軌所屬的相簿（例如，`"Pinegrove"`）。 用它來彙總相同專輯中各個曲目的參與度。

## 如何填入此維度

相簿是在工作階段開始時由播放器針對音訊內容所設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.album`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## 維度項目

每個專案都是工作階段開始時所回報的常值相簿標題。 來自不同藝人的兩張相同標題的專輯摺疊為單一行專案。 與[藝人](artist.md)維度配對，以去除混淆。
