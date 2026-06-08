---
title: 章節位置
description: 報告內容內每個章節的索引。
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# 章節位置

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**章節位置**&#x200B;報告維度。 請參閱[章節位置](/help/implementation/variables/chapters/chapter-position.md)以瞭解如何收集此變數。*

>[!ENDSHADEBOX]

**章節位置**&#x200B;維度會報告內容內每個章節的索引。

## 如何填入此維度

播放器在每個[章節開始](/help/implementation/events/chapters/chapter-start.md)事件上設定章節位置。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.chapter.position`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [Chapter](chapter.md)維度的分類。 為報表套裝啟用&#x200B;**[[!UICONTROL 媒體章節]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.chapter.position`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 媒體章節]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立章節位置分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個章節ID與其位置之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更章節位置分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.chapter.position`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取章節位置作為每次點選值，而不需要分類維護。

取捨是您會失去章節位置與上層[章節](chapter.md)維度之間保證的1:1關係。 如果您的實施在事件間傳送的相同章節ID值不一致，則同一章節下可能會出現多個位置。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是在[章節開始](/help/implementation/events/chapters/chapter-start.md)報告的整數位置值。
