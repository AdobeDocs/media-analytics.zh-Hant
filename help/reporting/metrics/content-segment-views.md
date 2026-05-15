---
title: 內容區段檢視次數
description: 計算發生作用中主要內容播放的區段。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 9%

---


# 內容區段檢視次數

**內容區段檢視**&#x200B;量度會計入發生使用中主要內容播放的五分鐘內容區段。 此量度可確認檢視器是否播放該區段中的內容，而不僅僅是載入或緩衝。 將其與[內容區段](/help/reporting/dimensions/content-segment.md)維度配對，以劃分長格式內容檢視器實際使用的部分。

## 此量度的計算方式

媒體後端會針對任何涵蓋區段的關閉呼叫設定`mediaReporting.sessionDetails.hasSegmentView = true`，其中至少已收到主要內容的一個[播放](/help/implementation/events/playback/play.md)事件。 量度會在關閉呼叫時回報。 在Media Edge API路徑上，區段檢視會在與內容開始的相同條件下引發。 這兩者都需要在主要內容上進行[播放](/help/implementation/events/playback/play.md)事件。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.segmentView`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
