---
title: Pod名稱
description: 報告每個廣告插播的易記名稱。 使用分類或自訂處理規則在Adobe Analytics中收集。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Pod名稱

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**Pod名稱**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告插播名稱](/help/implementation/variables/ads/ad-break-name.md)。*

>[!ENDSHADEBOX]

**Pod名稱**&#x200B;維度會報告每個廣告插播的易記名稱（例如，`"pre-roll"`、`"mid-roll-1"`）。 在Customer Journey Analytics中，這是直接從實作變數填入的分散維度。 在Adobe Analytics中，此功能可透過兩種方法提供： [廣告Pod](ad-pod.md)維度的分類，或使用處理規則填入的eVar。

## 如何填入此維度

Pod名稱來源為播放器在[廣告插播開始](/help/implementation/events/ads/ad-break-start.md)設定的[廣告插播名稱](/help/implementation/variables/ads/ad-break-name.md)值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.ad.podFriendlyName`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | 廣告Pod維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.podFriendlyName`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/setup/analytics-reporting.md)**&#x200B;時，Adobe會自動建立Pod名稱分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個Pod ID與其好記名稱之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更Pod名稱分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.ad.podFriendlyName`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取好記名稱作為每次點選值，而不需要分類維護。

取捨是您會遺失Pod名稱和上層[廣告Pod](ad-pod.md)維度之間保證的1:1關係。 如果您的實施在跨事件中針對同一個Pod ID傳送不一致的值，則同一廣告Pod下可能會出現多個名稱。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是在[廣告插播開始](/help/implementation/events/ads/ad-break-start.md)上報告的常值廣告插播名稱。
