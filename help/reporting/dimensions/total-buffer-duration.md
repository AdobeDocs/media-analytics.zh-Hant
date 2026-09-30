---
title: 總緩衝期間（維度）
description: 報告每個工作階段緩衝所花費的累積秒數。
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
source-wordcount: '194'
ht-degree: 7%
---

# 總緩衝期間（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**總緩衝期間**&#x200B;維度。 Adobe Analytics會從相同的`a.media.qoe.bufferTime`內容資料變數自動填入配對的[總緩衝期間（量度）](/help/reporting/metrics/total-buffer-duration.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.bufferTime`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**總緩衝期間**&#x200B;維度會報告播放器在工作階段期間花費在緩衝狀態的累積時間（以秒為單位）。 使用維度，可透過確切的緩衝期間值來劃分參與。

## 如何填入此維度

媒體後端會加總每個緩衝間隔（從[緩衝開始](/help/implementation/events/playback/buffer-start.md)到下一個狀態變更）的持續時間。 此值會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.bufferTime`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## 維度項目

每個專案都是關閉呼叫時回報的常值持續時間值（以秒為單位）。
