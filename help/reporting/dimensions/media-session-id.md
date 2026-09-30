---
title: 媒體工作階段ID
description: 唯一識別每個播放工作階段。
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
source-wordcount: '205'
ht-degree: 6%
---

# 媒體工作階段ID

**媒體工作階段識別碼**&#x200B;維度會唯一識別每個播放工作階段。 它由後端產生，並會在工作階段的每個事件上加上戳記。 用它來隔離單一工作階段的事件，以進行偵錯，或在自訂分析中刪除重複工作階段。

## 如何填入此維度

當後端收到[工作階段開始](/help/implementation/events/session/session-start.md)事件時，會自動產生工作階段識別碼。 Web SDK和Mobile SDK實作會擷取並保留您的ID；直接API實作必須從`sessionStart`回應（Media Collection API的`Location`標頭或Media Edge API的`media-analytics:new-session`控制代碼）讀取工作階段ID，並將其納入後續事件。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.vsid`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## 維度項目

每個專案都是後端產生的唯一工作階段ID （通常是22個字元的英數字串）。 使用「篩選」或「搜尋」欄位來查詢特定工作階段。
