---
title: 內容區段
description: 報告工作階段期間檢視的播放點範圍（以分鐘為單位）。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---


# 內容區段

**內容區段**&#x200B;維度會報告工作階段期間所檢視的播放點範圍（以分鐘為單位，例如`[0-5]`代表分鐘0到5）。 後端會根據播放期間回報的最小和最大播放點值來計算區段。 將其與[內容區段檢視](/help/reporting/metrics/content-segment-views.md)量度搭配使用，以分析長格式內容檢視器實際使用哪些部分。

## 如何填入此維度

內容區段是由媒體後端從工作階段事件中報告的播放點值計算。 使用者端並未設定。 報告的值衍生自播放期間所看到的播放點值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.segment`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videosegment, post_videosegment` |

>[!IMPORTANT]
>
>如果工作階段期間未正確報告播放點，則計算的區段可能不準確。 對於即時資料流，區段是根據在工作階段期間看到的相對播放點值計算而得。

## 維度項目

每個專案都是字串範圍，涵蓋工作階段期間所看到的播放點值（例如，`[0-5]`、`[5-10]`、`[10-15]`）。 詳細程度會固定在5分鐘。
