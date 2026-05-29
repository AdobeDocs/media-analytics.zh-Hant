---
title: 錯誤
description: 報告每個工作階段的錯誤事件計數。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# 錯誤

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**錯誤**維度。 Adobe Analytics會從相同的`a.media.qoe.errorCount`內容資料變數自動填入配對的[錯誤事件量度](/help/reporting/metrics/error-events.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.errorCount`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**Errors**&#x200B;維度會報告工作階段期間收到的錯誤事件計數。 使用維度可依確切錯誤計數劃分參與。

## 如何填入此維度

媒體後端會遞增播放器回報之每個錯誤的計數。 此值會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.errorCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## 維度項目

每個專案都是關閉呼叫時回報的常值錯誤計數值。 對於工作階段層級的布林值報告（無論是否發生任何錯誤），請使用[錯誤影響的資料流](/help/reporting/metrics/error-impacted-streams.md)。 如需唯一的錯誤ID，請使用[外部錯誤ID](external-error-ids.md)和[播放器SDK錯誤ID](player-sdk-error-ids.md)。

>[!NOTE]
>
>如果您使用舊版心率SDK (Media SDK 1.5.x-2.x)，SDK內部產生的錯誤ID會自動收集在內容資料索引鍵`a.media.qoe.mediaSdkErrors`下，並可透過自訂處理規則在Adobe Analytics中存取。 Audience Manager特徵是`c_contextdata.a.media.qoe.mediaSdkErrors`。 此欄位不適用於Media Collection API或Media Edge API實施。
