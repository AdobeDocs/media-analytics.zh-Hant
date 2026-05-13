---
title: 受子母畫面影響的資料流
description: 計算檢視器至少一次輸入子母畫面的工作階段數。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---


# 受子母畫面影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受子母畫面影響的&#x200B;**資料流**&#x200B;報告量度。 如需如何收集此變數，請參閱[子母畫面](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**受子母畫面影響的資料流**&#x200B;量度會計算檢視器至少一次進入子母畫面播放的工作階段。 量度是工作階段層級的布林值 — 在相同工作階段中，多個子母畫面專案會計為一個受影響的資料流。 若要取得子母畫面輸入的總數量，請使用[子母畫面計數](picture-in-picture-count.md)。

## 此量度的計算方式

媒體後端在第一次收到`statesStart`中具有`pictureInPicture`的`media.statesUpdate`事件時，將`pictureInPicture`專案的`mediaReporting.states[]`中的`isSet`旗標設為`true`。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.pictureinpicture.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "pictureInPicture"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
