---
title: 內容長度
description: 報告每個媒體工作階段在工作階段開始時所設定的總持續時間（秒數）。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# 內容長度

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容長度**&#x200B;報告維度。 如需如何收集此變數，請參閱[內容長度](/help/implementation/variables/core/content-length.md)。*

>[!ENDSHADEBOX]

**內容長度**&#x200B;維度會報告每個媒體工作階段在工作階段開始時設定的總持續時間（秒數）。 它支援後端量度，包括[進度標籤](/help/reporting/metrics/progress-markers.md)和[平均每分鐘觀眾數](/help/reporting/metrics/average-minute-audience.md)。

## 如何填入此維度

內容長度由播放器在工作階段開始時設定。 報告的值是資產的完整持續時間（以秒為單位），而不是經過的播放點。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.length`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>在Adobe Analytics中，此值也對應至[Content](content.md)維度上的&#x200B;**影片長度**&#x200B;分類。 您需個別負責填入及維護該分類。 Customer Journey Analytics直接使用此維度。 您可以視需要使用[值分組](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing)。

>[!IMPORTANT]
>
>如果未設定內容長度，或未大於零，則不會為該工作階段產生進度標籤和平均每分鐘觀眾數。 對於持續時間不明的即時資料流，請設定`86400`。

## 維度項目

每個專案都是工作階段開始時回報的常值長度值（以秒為單位）。
