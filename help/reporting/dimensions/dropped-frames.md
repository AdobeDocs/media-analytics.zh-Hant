---
title: 掉格（維度）
description: 報告每個工作階段的累計掉格計數。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---


# 掉格（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**掉格**維度。 Adobe Analytics會從相同的`a.media.qoe.droppedFrameCount`內容資料變數自動填入配對的[掉格（量度）](/help/reporting/metrics/dropped-frames.md)。 Customer Journey Analytics公開單一`mediaReporting.qoeDataDetails.droppedFrames`欄位，您可將其作為維度或量度使用。 如需如何收集此變數，請參閱[掉格](/help/implementation/variables/quality/dropped-frames.md)。*

>[!ENDSHADEBOX]

**掉格**&#x200B;維度會報告工作階段期間掉格的累計計數。 使用維度，可透過確切的下拉計數來劃分參與。

## 如何填入此維度

播放器會在累積捨棄時更新QoE物件的`droppedFrames`值。 後端會報告關閉呼叫的最新值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.droppedFrameCount`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## 維度項目

每個專案都是結束呼叫時回報的常值下降值。 對於工作階段層級的布林報表（無論是否有任何影格被卸除），請使用[受影響的](/help/reporting/metrics/dropped-frame-impacted-streams.md)個卸除影格。
