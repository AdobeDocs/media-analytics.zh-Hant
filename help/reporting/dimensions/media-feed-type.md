---
title: 媒體摘要型別
description: 透過多個摘要提供相同內容時，會報告廣播摘要（例如East-HD或West-SD）。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# 媒體摘要型別

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**媒體摘要型別**&#x200B;報告維度。 如需如何收集此變數，請參閱[媒體摘要型別](/help/implementation/variables/standard-metadata/media-feed-type.md)。*

>[!ENDSHADEBOX]

**媒體摘要型別**&#x200B;維度會報告每個工作階段的廣播摘要（例如，`"East-HD"`、`"West-SD"`或`"4K"`）。 當透過多個區域或品質摘要提供相同內容，且每個摘要需要報告參與時，請使用它。

## 如何填入此維度

媒體摘要型別是由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.feed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## 維度項目

每個專案是在工作階段開始時報告的常值摘要值。 根據地區或品質分割使用一組穩定的摘要識別碼。
