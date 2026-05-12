---
title: 創作者
description: 報告內容的建立者或生產工作室。
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---


# 創作者

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**創作者**&#x200B;報告維度。 請參閱[建立者](/help/implementation/variables/standard-metadata/originator.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**創作者**&#x200B;維度會報告內容的建立者或製作工作室（例如，`"Warner Brothers"`或`"Sony"`）。 用它來比較內容擁有者或權利持有者的參與情形。

## 如何填入此維度

創作者在工作階段開始時由播放器設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.originator`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [內容（識別碼）](content.md)維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.originator`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立建立建立者分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個內容ID與其建立者之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更建立者分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.originator`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會將建立者擷取為每次點選值，而不需要分類維護。

取捨是您會遺失建立者與上層[內容（識別碼）](content.md)維度之間保證的1:1關係。 如果您的實施在不同事件間為相同的內容ID傳送不一致的值，則相同內容下可能會出現多個建立者。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是工作階段開始時所回報的常值建立者值。 每個工作室使用穩定、不同的名稱，以便參與不會跨不相關的實體摺疊。
