---
title: 內容分級
description: 依美國電視分級制度(TV Parental Guidelines)或地區分級系統的定義，報告對象分級。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---


# 內容分級

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容評等**&#x200B;報告維度。 如需如何收集此變數，請參閱[內容評等](/help/implementation/variables/standard-metadata/content-rating.md)。*

>[!ENDSHADEBOX]

**內容評等**&#x200B;維度會報告每個工作階段的對象評等。 用它來比較不同評等層級的參與度和廣告負載。

## 如何填入此維度

內容評等由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.rating`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [內容（識別碼）](content.md)維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.rating`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.rating` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立內容評等分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個內容ID與其評等之間都有1:1關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更內容評等分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.rating`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取每次點選值的內容評分，而不需要分類維護。

取捨是您會失去內容評等與上層[內容（識別碼）](content.md)維度之間保證的1:1關係。 如果您的實施在不同事件間為相同的內容ID傳送不一致的值，則相同內容下可能會顯示多個評等。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是工作階段開始時報告的常值評等值（例如，`"TVY"`、`"TVG"`、`"TVPG"`、`"TVMA"`）。 遵循每個評等系統的固定值集，以避免分割條列專案。
