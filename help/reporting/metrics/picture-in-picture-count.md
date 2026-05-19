---
title: 子母畫面次數
description: 報告檢視者在工作階段期間輸入子母畫面次數。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# 子母畫面次數

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**子母畫面計數**&#x200B;報告量度。 如需如何收集此變數，請參閱[子母畫面](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**子母畫面計數**&#x200B;量度會報告檢視者在工作階段期間進入子母畫面播放的次數。 每個子母畫面狀態開始事件都會增加計數。 配對[受子母畫面影響的資料流](picture-in-picture-streams-impacted.md)，以進行工作階段層級的布林值統計，並配對[子母畫面總持續時間](picture-in-picture-total-duration.md)，以進行狀態總時間。

## 此量度的計算方式

媒體後端會遞增每個子母畫面狀態開始事件的此計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 播放器狀態追蹤]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.states.pictureinpicture.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)專案，其中`name = "pictureInPicture"`，欄位`count` |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
