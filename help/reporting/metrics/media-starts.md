---
title: 媒體開始
description: 計算開始的每個媒體工作階段，包括以前段廣告或緩衝結束的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 媒體開始

**媒體開始**&#x200B;量度會計算每個開始的媒體工作階段。 後端收到`media.sessionStart`事件時，即使檢視器在前段廣告、緩衝或任何主要內容播放之前退出，也會增加事件數量。 將它當做媒體報表最廣泛的funnel頂端量度；將其與[Content starts](content-starts.md)配對，以測量廣告和緩沖流失。

## 此量度的計算方式

收到`media.sessionStart`事件時，媒體後端會設定`mediaReporting.sessionDetails.isViewed = true`。 報告的量度是每個工作階段`1`。 媒體開始次數是報告在開始呼叫上，而不是報告在關閉呼叫上。 這是唯一不會等待工作階段關閉的階段1量度。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.view`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
