---
title: 節目型別
description: 報告內容格式（全集、預覽、剪輯或其他）。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# 節目型別

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**節目型別**&#x200B;報告維度。 如需如何收集此變數，請參閱[顯示型別](/help/implementation/variables/standard-metadata/show-type.md)。*

>[!ENDSHADEBOX]

**顯示型別**&#x200B;維度使用字串整數代碼來報告內容格式。 在測量參與度時，使用它可將完整程式檢視與短格式內容（如預告片和剪輯）分開。

## 如何填入此維度

節目型別由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.type`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoshowtype, post_videoshowtype` |

## 維度項目

| 值 | 說明 |
| --- | --- |
| `0` | 全集 |
| `1` | 預覽或預告 |
| `2` | Clip |
| `3` | 其他 |

值會回報為字串。 接受自訂值，但不會彙總到四個內建值區中。
