---
title: 掉格（維度）
description: 報告每個工作階段的累計掉格計數。
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
source-wordcount: '183'
ht-degree: 7%
---

# 掉格（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**掉格**&#x200B;維度。 Adobe Analytics會從相同的`a.media.qoe.droppedFrameCount`內容資料變數自動填入配對的[掉格（量度）](/help/reporting/metrics/dropped-frames.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.droppedFrames`欄位，您可將其作為維度或量度使用。 如需如何收集此變數，請參閱[掉格](/help/implementation/variables/quality/dropped-frames.md)。*

>[!ENDSHADEBOX]

**掉格**&#x200B;維度會報告工作階段期間掉格的累計計數。 使用維度，可透過確切的下拉計數來劃分參與。

## 如何填入此維度

播放器會在累積捨棄時更新QoE物件的`droppedFrames`值。 後端會報告關閉呼叫的最新值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.droppedFrameCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## 維度項目

每個專案都是結束呼叫時回報的常值下降值。 對於工作階段層級的布林報表（無論是否有任何影格被卸除），請使用[受影響的](/help/reporting/metrics/dropped-frame-impacted-streams.md)個卸除影格。
