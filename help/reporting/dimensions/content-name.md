---
title: 內容名稱
description: 報告每個媒體工作階段的人類可讀標題。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 10%

---


# 內容名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容名稱**&#x200B;報告維度。 如需如何收集此變數，請參閱[內容名稱](/help/implementation/variables/core/content-name.md)。*

>[!ENDSHADEBOX]

**內容名稱**&#x200B;維度會報告每個媒體工作階段的人類可讀標題。

## 如何填入此維度

易記名稱由播放器在工作階段開始時設定。 報告的值與傳送的內容相符。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.friendlyName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>在Adobe Analytics中，此值也對應至[Content](content.md)維度上的&#x200B;**影片名稱**&#x200B;分類。 您需個別負責填入及維護該分類。 Customer Journey Analytics直接使用此維度。

>[!IMPORTANT]
>
>如果未設定內容名稱，則會針對該工作階段取消填入維度。

## 維度項目

每個專案都是工作階段開始時報告的常值標題（例如，`"Blinding Light"`）。
