---
title: 廣告載入
description: 報告用於每個串流媒體工作階段的廣告載入型別。
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
source-wordcount: '161'
ht-degree: 8%
---

# 廣告載入

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告載入**報告維度。 如需如何收集此變數，請參閱[廣告載入型別](/help/implementation/variables/standard-metadata/ad-load-type.md)。*

>[!ENDSHADEBOX]

**廣告載入**&#x200B;維度會報告在每個串流媒體工作階段開始時載入的廣告型別。 此值由客戶定義，可讓組織透過其廣告傳遞機制（例如，`"linear"`、`"dynamic"`或`"programmatic"`）來分類工作階段。

## 如何填入此維度

廣告載入型別由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 設定[[!UICONTROL 串流媒體]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.adLoad`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## 維度項目

每個專案都是工作階段開始時所設定的常值廣告載入型別字串。 值不受限於標準列舉。 定義在您的實施中一致的分類法，讓值以可預見的方式在報表中累計。
