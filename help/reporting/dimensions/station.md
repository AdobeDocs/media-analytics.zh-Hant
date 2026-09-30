---
title: 電台
description: 報告音訊廣播內容的廣播電台名稱或ID。
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
source-wordcount: '138'
ht-degree: 10%
---

# 電台

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**電台**報告維度。 請參閱[工作站](/help/implementation/variables/standard-metadata/station.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**電台**&#x200B;維度會報告廣播音訊內容的廣播電台名稱或識別碼（例如，`"NPR"`或`"WXYZ-FM"`）。 用它來比較聯合網路中跨站台的參與度。

## 如何填入此維度

播放器在工作階段開始時為音訊內容設定電台。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.station`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## 維度項目

每個專案都是工作階段開始時報告的常值工作站名稱或ID。 每個站台使用單一標準識別碼，參與就不會在呼叫符號變體間分段。
