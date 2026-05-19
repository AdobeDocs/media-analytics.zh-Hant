---
title: 子母畫面總時間
description: 報告檢視者在工作階段期間用於子母畫面顯示的累計秒數。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---


# 子母畫面總時間

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**子母畫面總時間**&#x200B;報告量度。 如需如何收集此變數，請參閱[子母畫面](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**子母畫面總持續時間**&#x200B;量度會報告檢視者在工作階段期間子母畫面所花費的累積時間（以秒為單位）。 後端會加總子母畫面狀態開始與相符狀態結束事件之間的每個間隔。

## 此量度的計算方式

媒體後端會加總工作階段期間所有子母畫面間隔的經過時間。 量度會在關閉呼叫時回報。 Analysis Workspace將值顯示為`HH:MM:SS`；資料摘要、Data Warehouse及報表API將以秒為單位顯示該值。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.pictureinpicture.time`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "pictureInPicture"`，欄位`time` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
