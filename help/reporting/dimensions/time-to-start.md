---
title: 開始時間（維度）
description: 報告轉譯第一個影格之前經過的時間。
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
source-wordcount: '190'
ht-degree: 7%
---

# 開始時間（維度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**開始時間**&#x200B;維度。 Adobe Analytics會從相同的`a.media.qoe.timeToStart`內容資料變數自動填入配對的[開始時間（量度）](/help/reporting/metrics/time-to-start.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.timeToStart`欄位，您可將其作為維度或量度使用。 如需如何收集此變數，請參閱[開始時間](/help/implementation/variables/quality/time-to-start.md)。*

>[!ENDSHADEBOX]

**開始時間**&#x200B;維度會報告從工作階段開始到第一個影格轉譯之間經過的時間。 使用維度可依啟動時段劃分參與專案。 Adobe會以秒為單位儲存值，並在擷取時從播放器報表轉換毫秒。

## 如何填入此維度

在工作階段開始引發之前，播放器會設定QoE物件上的`timeToStart`。 後端會報告關閉呼叫的值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.qoe.timeToStart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## 維度項目

每個專案都是關閉呼叫時回報的常值啟動時間值。
