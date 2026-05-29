---
title: 緩衝事件（量度）
description: 計算各工作階段總和平均值的緩衝事件。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# 緩衝事件（量度）

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**緩衝事件**量度。 Adobe Analytics會從相同的`a.media.qoe.bufferCount`內容資料變數自動填入配對的[緩衝事件（維度）](/help/reporting/dimensions/buffer-events.md)。 Customer Journey Analytics公開單一`xdm.mediaReporting.qoeDataDetails.bufferCount`欄位，您可將其作為維度或量度使用。*

>[!ENDSHADEBOX]

**緩衝事件**&#x200B;量度會計算各工作階段的緩衝事件，適用於總和、平均值及百分位數統計。 使用量度可計算報告期間的總緩衝量，並比較內容、網路或播放器間的緩衝穩定性。

## 此量度的計算方式

每次播放器進入[緩衝開始](/help/implementation/events/playback/buffer-start.md)狀態時，媒體後端都會增加計數。 量度會在關閉呼叫時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體品質]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.qoe.bufferCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

對於工作階段層級的布林值報告（工作階段是否遇到任何緩衝），請使用[緩衝影響的資料流](buffer-impacted-streams.md)。
