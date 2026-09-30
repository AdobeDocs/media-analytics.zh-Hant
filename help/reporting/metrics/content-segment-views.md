---
title: 內容區段檢視次數
description: 計算發生作用中主要內容播放的區段。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 9%
---

# 內容區段檢視次數

**內容區段檢視**&#x200B;量度會計入發生使用中主要內容播放的五分鐘內容區段。 此量度可確認檢視器是否播放該區段中的內容，而不僅僅是載入或緩衝。 將其與[內容區段](/help/reporting/dimensions/content-segment.md)維度配對，以劃分長格式內容檢視器實際使用的部分。

## 此量度的計算方式

媒體後端會為任何涵蓋區段的關閉呼叫設定此旗標，其中至少已收到主要內容的一個[播放](/help/implementation/events/playback/play.md)事件。 量度會在關閉呼叫時回報。 在Media Edge API路徑上，區段檢視會在與內容開始的相同條件下引發。 這兩者都需要在主要內容上進行[播放](/help/implementation/events/playback/play.md)事件。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.segmentView`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | 不適用 |
