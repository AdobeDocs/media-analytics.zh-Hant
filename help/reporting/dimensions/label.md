---
title: 標籤
description: 報告發行音訊內容的唱片標籤。
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
source-wordcount: '134'
ht-degree: 10%
---

# 標籤

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**標籤**&#x200B;報告維度。 請參閱[標籤](/help/implementation/variables/standard-metadata/label.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**Label**&#x200B;維度會報告發行音訊內容的唱片標籤（例如，`"Capitol Records"`）。 用它來比較音樂或播客目錄中不同標籤的參與度。

## 如何填入此維度

標籤是在工作階段開始時由播放器針對音訊內容設定的。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 音訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.label`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## 維度項目

每個專案都是工作階段開始時回報的常值標簽名稱。 每個標籤使用穩定、規範的名稱，這樣參與就不會在拼字或壓印變體之間產生碎片。
