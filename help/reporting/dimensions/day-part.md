---
title: 時段
description: 報告廣播或播放內容時的當天時段（上午、下午、黃金時段、深夜）。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 8%

---


# 時段

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**天部分**&#x200B;報告維度。 如需如何收集此變數，請參閱[Day part](/help/implementation/variables/standard-metadata/day-part.md)。*

>[!ENDSHADEBOX]

**天部分**&#x200B;維度會報告內容廣播或播放時的當天時段。 通用值為`"Morning"`、`"Afternoon"`、`"Primetime"`和`"Late Night"`。 用它來比較不同日段的參與，不受檢視者當地時區的影響。

## 如何填入此維度

白天部分由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.dayPart`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## 維度項目

每個專案都是工作階段開始時報告的常值時段。 在實作中使用固定的值集，以保持條列專案的一致性。
