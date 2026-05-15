---
title: 首播日期
description: 報告內容在電視上的首播日期。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# 首播日期

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**首播日期**&#x200B;報告維度。 如需如何收集此變數，請參閱[首播日期](/help/implementation/variables/standard-metadata/first-air-date.md)。*

>[!ENDSHADEBOX]

**首播日期**&#x200B;維度會報告內容在電視上的首播日期。 使用它可將新版本的參與度與舊內容的參與度分開。

## 如何填入此維度

首次播放日期由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.airDate`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [內容（識別碼）](content.md)維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.airDate`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.airDate` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立First air日期分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個內容ID與其首次播放日期之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更首播日期分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.airDate`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會將首次播放日期擷取為每次點選值，而不需要分類維護。

取捨是您會失去第一個播放日期與上層[內容（識別碼）](content.md)維度之間保證的1:1關係。 如果您的實施在跨事件中針對相同的內容ID傳送不一致的值，則相同內容下可能會出現多個首次播放日期。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是工作階段開始時所回報的常值日期字串。 在實作中使用一致的格式。 Adobe建議`YYYY-MM-DD`。
