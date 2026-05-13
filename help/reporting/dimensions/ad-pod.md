---
title: 廣告Pod
description: 報告每個獨特的廣告插播，由自動產生的Pod ID作為索引鍵。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# 廣告Pod

**廣告Pod**&#x200B;維度會報告每個以自動產生的Pod ID作為索引鍵的唯一廣告插播。 工作階段中的每個廣告都屬於上層廣告Pod，而Pod會將多個播放的廣告連續分組。 使用維度來透過廣告插播中斷參與，並當作[Pod名稱](pod-name.md)和[Pod位置](pod-position.md)分類的聯結索引鍵。

## 如何填入此維度

當`media.adBreakStart`引發時，SDK會自動產生廣告Pod ID。 直接API實作會從中斷索引和開始時間建構它，或提供自訂pod ID。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體廣告]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.ad.pod`收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 資料饋送 | `videoadpod, post_videoadpod` |

## 維度項目

每個專案都是不重複的廣告Pod ID。 ID不透明（通常是工作階段ID、內容ID和中斷索引的雜湊），在與[Pod名稱](pod-name.md)結合使用時作為好記標籤的分組索引鍵最有用。
