---
title: 創作 ID
description: 報告廣告創意識別碼。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 3%

---


# 創作 ID

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**Creative ID**&#x200B;報告維度。 如需如何收集此變數，請參閱[Creative ID](/help/implementation/variables/ads/creative-id.md)。*

>[!ENDSHADEBOX]

**Creative ID**&#x200B;維度會報告廣告創意識別碼。 使用維度可在共用創意的廣告間彙總參與度。

## 如何填入此維度

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.ad.creative`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [廣告](ad.md)維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.creative`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立Creative ID分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個廣告ID與其創意ID之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更Creative ID分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.ad.creative`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取創意ID作為每次點選值，而不需要分類維護。

取捨是您會遺失創意ID與上層[廣告](ad.md)維度之間保證的1:1關係。 如果您的實施在不同事件間為相同的廣告ID傳送不一致的值，則同一廣告下可能會出現多個創意ID。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是唯一的創意ID。 對每個創意內容使用穩定的識別碼，以便相同的創意內容跨行銷活動向上彙整為單一條列專案。
