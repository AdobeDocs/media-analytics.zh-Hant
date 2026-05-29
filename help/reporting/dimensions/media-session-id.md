---
title: 媒體工作階段ID
description: 唯一識別每個播放工作階段。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# 媒體工作階段ID

**媒體工作階段識別碼**&#x200B;維度會唯一識別每個播放工作階段。 它由後端產生，並會在工作階段的每個事件上加上戳記。 用它來隔離單一工作階段的事件，以進行偵錯，或在自訂分析中刪除重複工作階段。

## 如何填入此維度

當後端收到[工作階段開始](/help/implementation/events/session/session-start.md)事件時，會自動產生工作階段識別碼。 Web SDK和Mobile SDK實作會擷取並保留您的ID；直接API實作必須從`sessionStart`回應（Media Collection API的`Location`標頭或Media Edge API的`media-analytics:new-session`控制代碼）讀取工作階段ID，並將其納入後續事件。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.vsid`對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## 維度項目

每個專案都是後端產生的唯一工作階段ID （通常是22個字元的英數字串）。 使用「篩選」或「搜尋」欄位來查詢特定工作階段。
