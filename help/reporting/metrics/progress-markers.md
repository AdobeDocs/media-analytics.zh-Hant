---
title: 進度標籤
description: 計算其播放點超過五個固定臨界值（10%、25%、50%、75%和95%）中每一個的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 7%

---


# 進度標籤

**進度標籤**&#x200B;是五個個別的量度，會計算播放點超過五個固定臨界值（內容長度的10%、25%、50%、75%和95%）各一的工作階段。 使用它們繪製內容執行階段中的流失圖表；與[內容開始](content-starts.md)配對，以計算到達每個里程碑之已啟動工作階段的份額。

每個標籤會在每個工作階段引發一次，而且不會在向後搜尋時重新觸發。 向前搜尋時跳過的標籤不會計入（例如，從5%跳到60%的檢視者會同時觸發10%、25%和50%標籤）。

## 如何計算每個標籤

媒體後端會在每個事件之後根據`Content length`評估報告的播放點。 當播放點第一次超過臨界值時，在工作階段的其餘時間內，對應的`mediaReporting.sessionDetails.hasProgress*`布林值會設為`true`。 所有五個標籤都會在結束通話時回報。

### 10%進度標籤 {#progress-10}

當播放點首次達到內容長度的10%時引發。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.progress10`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |

### 25%進度標籤 {#progress-25}

當播放點首次達到內容長度的25%時引發。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.progress25`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |

### 50%進度標籤 {#progress-50}

當播放點首次達到內容長度的50%時引發。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.progress50`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |

### 75%進度標籤 {#progress-75}

當播放點首次達到內容長度的75%時引發。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.progress75`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |

### 95%進度標籤 {#progress-95}

當播放點首次達到內容長度的95%時引發。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.progress95`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |

>[!IMPORTANT]
>
>進度標籤需要非零的[內容長度](/help/reporting/dimensions/content-length.md)和精確的播放點報告。 如果內容長度未設定、為零或錯誤，則標籤可能會在錯誤的時間引發，或完全不會引發。
