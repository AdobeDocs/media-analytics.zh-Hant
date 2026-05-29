---
title: Pod位置
description: 報告內容內每個廣告插播的位移。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Pod位置

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**Pod位置**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告插播開始時間](/help/implementation/variables/ads/ad-break-start-time.md)。*

>[!ENDSHADEBOX]

**Pod位置**&#x200B;維度會報告內容內每個廣告插播的位移（以秒為單位）。 前段具有位置`0`；中間段具有與其播放點開始時間相對應的位置。

## 如何填入此維度

Pod位置是從播放器在[廣告插播開始](/help/implementation/events/ads/ad-break-start.md)設定的[廣告插播開始時間](/help/implementation/variables/ads/ad-break-start-time.md)值設定的。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics （處理規則） | 建立將`a.media.ad.podSecond`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics （分類） | [廣告Pod](ad-pod.md)維度的分類 — 為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立此分類。 您需負責填入及維護分類值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 資料摘要（處理規則） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.ad.podSecond`對應至的eVar） |
| 資料摘要（分類） | 不適用 — 資料摘要不支援分類。 |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## 分類方法

為報表套裝啟用&#x200B;**[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)**&#x200B;時，Adobe會自動建立Pod位置分類結構。 您負責使用[分類設定](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填入及維護分類。

此方法可保證每個廣告Pod ID與其位置之間有1:1個關係。 分類更新會回溯套用至該ID的所有歷史資料。

>[!IMPORTANT]
>
>請勿變更Pod位置分類名稱。 將其重新命名可能會導致Adobe重新建立原始分類，並造成重複。

## 處理規則方法

建立將`a.media.ad.podSecond`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法會擷取pod位置作為每次點選值，而不需要分類維護。

取捨是您會遺失pod位置與上層[廣告pod](ad-pod.md)維度之間保證的1:1關係。 如果您的實施在跨事件中針對同一個Pod ID傳送不一致的值，則同一廣告Pod下可能會出現多個位置。 更新值僅適用於未來的資料。

## 維度項目

每個專案都是[廣告插播開始](/help/implementation/events/ads/ad-break-start.md)所報告的整數位移值（以秒為單位）。
