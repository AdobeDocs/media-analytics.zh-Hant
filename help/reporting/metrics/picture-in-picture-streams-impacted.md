---
title: 受子母畫面影響的資料流
description: 計算檢視器至少一次輸入子母畫面的工作階段數。
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
source-wordcount: '192'
ht-degree: 7%
---

# 受子母畫面影響的資料流

>[!BEGINSHADEBOX]

*此頁面涵蓋受子母畫面影響的&#x200B;**資料流**報告量度。 如需如何收集此變數，請參閱[子母畫面](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**受子母畫面影響的資料流**&#x200B;量度會計算檢視器至少一次進入子母畫面播放的工作階段。 量度是工作階段層級的布林值；相同工作階段中的多個子母畫面專案會計為一個受影響的資料流。 若要取得子母畫面輸入的總數量，請使用[子母畫面計數](picture-in-picture-count.md)。

## 此量度的計算方式

媒體後端會在工作階段期間第一次收到子母畫面狀態開始事件時設定此旗標。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.states.pictureinpicture.set`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "pictureInPicture"`，欄位`isSet` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
