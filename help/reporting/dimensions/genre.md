---
title: 類型
description: 報告內容型別。 多型別內容會跨條列專案分割，每個條列專案會獲得相等的量度權重。
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
source-wordcount: '181'
ht-degree: 8%
---

# 類型

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**型別**報告維度。 如需如何收集此變數，請參閱[型別](/help/implementation/variables/standard-metadata/genre.md)。*

>[!ENDSHADEBOX]

**型別**&#x200B;維度會報告內容型別。 型別會以逗號分隔的字串形式收集，並儲存為清單維度。 多型別內容會分割為單獨的條列專案，每個條列專案會獲得相同的量度權重。 使用它來比較不同型別的參與度，而不需重複計算在單一多型別資產上所花費的時間。

## 如何填入此維度

型別是在工作階段開始時由播放器設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.genre` （儲存為清單變數）收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting)或[`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) （舊版） |
| 資料饋送 | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## 維度項目

每個專案都是一個型別值。 多型別工作階段（例如，`"Drama,Action"`）顯示為兩個獨立的條列專案（`Drama`和`Action`），每個專案都收到工作階段的完整評價。
