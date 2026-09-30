---
title: 資產 ID
description: 報告基礎媒體資產的穩定產業識別碼。
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
source-wordcount: '410'
ht-degree: 2%
---

# 資產 ID

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**資產識別碼**&#x200B;報告維度。 請參閱[資產識別碼](/help/implementation/variables/standard-metadata/asset-id.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**資產ID**&#x200B;維度會報告基礎媒體資產的穩定產業識別碼（通常是EIDR、TMS/Gracenote或Rovi ID，但也接受專有ID）。

## 如何填入此維度

資產ID是在工作階段開始時由播放器設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.asset`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [內容（識別碼）](content.md)維度的分類。 為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.asset`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.asset` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 視訊中繼資料]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立資產ID分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可確保每個內容ID與其資產ID之間維持1:1關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更資產ID分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.asset`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取資產ID作為每次點選值，而不需要分類維護。

取捨是您會失去資產ID與上層[內容(ID)](content.md)維度之間保證的1:1關係。 如果您的實施在不同事件間傳送的相同內容ID值不一致，則相同內容下可能會出現多個資產ID。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是報表期間所回報的唯一資產ID值。 跨所有發佈平台針對每個資產使用單一穩定識別碼，以便相同內容向上彙整至單一條列專案。
