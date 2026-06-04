---
title: 類型
description: 報告內容型別。 多型別內容會跨條列專案分割，每個條列專案會獲得相等的量度權重。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# 類型

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**型別**&#x200B;報告維度。 如需如何收集此變數，請參閱[型別](/help/implementation/variables/standard-metadata/genre.md)。*

>[!ENDSHADEBOX]

**型別**&#x200B;維度會報告內容型別。 型別會以逗號分隔的字串形式收集，並儲存為清單維度。 多型別內容會分割為單獨的條列專案，每個條列專案會獲得相同的量度權重。 使用它來比較不同型別的參與度，而不需重複計算在單一多型別資產上所花費的時間。

## 如何填入此維度

型別是在工作階段開始時由播放器設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.genre` （儲存為清單變數）收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting)或[`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) （舊版） |
| 資料饋送 | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## 維度項目

每個專案都是一個型別值。 多型別工作階段（例如，`"Drama,Action"`）顯示為兩個獨立的條列專案（`Drama`和`Action`），每個專案都收到工作階段的完整評價。
