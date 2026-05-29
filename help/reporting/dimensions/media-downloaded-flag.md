---
title: 媒體已下載
description: 標示播放已下載離線內容的工作階段。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 媒體已下載

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**下載的媒體**報告維度。 如需如何收集此變數，請參閱[媒體已下載的旗標](/help/implementation/variables/core/media-downloaded-flag.md)。*

>[!ENDSHADEBOX]

**下載的媒體**&#x200B;維度會標籤播放先前下載離線內容的工作階段，而非來自網際網路的即時資料流。 比較參與度、完成度或品質時，請使用它來將離線播放與串流工作階段分開。

## 如何填入此維度

播放器會透過下列三種方式之一設定下載的標幟。 使用旗標初始化追蹤器（行動SDK），將`sessionStart`傳送至`/downloaded`端點變體（Media Edge API直接），或在`sessionStart`引數（媒體收集API）中包含`media.downloaded: true`。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.downloaded`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.downloaded`對應至的eVar） |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## 維度項目

| 值 | 說明 |
| --- | --- |
| `true` | 工作階段已播放下載的離線內容。 |
| （空白） | 工作階段已播放即時資料流。 省略該欄位，而不是設為`false`。 |
