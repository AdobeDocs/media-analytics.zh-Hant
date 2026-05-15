---
title: 串流媒體事件概觀
description: 瞭解媒體事件型別及其必須傳送的順序。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# 串流媒體事件

串流媒體追蹤的運作方式是傳送一系列事件呼叫至Adobe資料收集端點，每個事件呼叫代表播放器狀態轉變。 每個事件都屬於以[sessionStart](session/session-start.md)呼叫開頭並以[sessionComplete](session/session-complete.md)或[sessionEnd](session/session-end.md)關閉的使用中工作階段。

## 事件工作流程

下列已排序清單顯示典型VOD播放的必要事件序列，其中包含一個前段廣告和一個章節：

1. **[工作階段開始](session/session-start.md)**：永遠是第一個事件；建立工作階段並傳回工作階段識別碼
2. **[廣告插播開始](ads/ad-break-start.md)**：任何廣告事件之前都需要
3. **[廣告開始](ads/ad-start.md)** → **[廣告完成](ads/ad-complete.md)** （或&#x200B;**[廣告略過](ads/ad-skip.md)**）
4. **[廣告插播完成](ads/ad-break-complete.md)**：插播中的所有廣告之後為必要
5. **[播放](playback/play.md)**：代表內容播放開始或繼續
6. **[章節開始](chapters/chapter-start.md)**：選擇性；標示章節開始
7. **[Ping](playback/ping.md)**：主要內容期間每10秒傳送一次，廣告期間每1秒傳送一次
8. **[章節完成](chapters/chapter-complete.md)**：選擇性；標籤章節的結尾
9. **[暫停開始](playback/pause-start.md)** → **[播放](playback/play.md)** （繼續）：任何暫停
10. **[緩衝開始](playback/buffer-start.md)** → **[播放](playback/play.md)** （繼續）：適用於任何緩衝
11. **[工作階段完成](session/session-complete.md)**：當檢視器到達內容結尾時

如果檢視者在到達內容結尾之前放棄工作階段，請使用[工作階段結束](session/session-end.md)，而非工作階段完成。

## 工作階段生命週期

如果符合下列任何條件，工作階段就會自動過期：

* **10分鐘未收到任何事件**
* **30分鐘沒有播放點移動**

## 事件參考

| 事件 | 類別 | 關聯的量度 |
| --- | --- | --- |
| [工作階段開始](session/session-start.md) | 工作階段 | [媒體開始](/help/reporting/metrics/media-starts.md) |
| [工作階段完成](session/session-complete.md) | 工作階段 | [內容完成](/help/reporting/metrics/content-completes.md) |
| [工作階段結束](session/session-end.md) | 工作階段 | — |
| [播放](playback/play.md) | 播放 | [內容開始](/help/reporting/metrics/content-starts.md) |
| [暫停開始](playback/pause-start.md) | 播放 | [暫停事件](/help/reporting/metrics/pause-events.md) |
| [緩衝開始](playback/buffer-start.md) | 播放 | [緩衝事件](/help/reporting/metrics/buffer-events.md) |
| [位元速率變更](playback/bitrate-change.md) | 播放 | [位元速率變更](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | 播放 | — |
| [廣告插播開始](ads/ad-break-start.md) | 廣告 | — |
| [廣告開始](ads/ad-start.md) | 廣告 | [廣告開始](/help/reporting/metrics/ad-starts.md) |
| [廣告完成](ads/ad-complete.md) | 廣告 | [廣告完成](/help/reporting/metrics/ad-completes.md) |
| [廣告略過](ads/ad-skip.md) | 廣告 | — |
| [廣告插播完成](ads/ad-break-complete.md) | 廣告 | — |
| [章節開始](chapters/chapter-start.md) | 章節 | [章節開始](/help/reporting/metrics/chapter-starts.md) |
| [章節完成](chapters/chapter-complete.md) | 章節 | [章節完成](/help/reporting/metrics/chapter-completes.md) |
| [章節略過](chapters/chapter-skip.md) | 章節 | — |
| [狀態開始](player-state/state-start.md) | 播放器狀態 | 因州而異 |
| [狀態結束](player-state/state-end.md) | 播放器狀態 | 因州而異 |
| [錯誤](error.md) | 品質 | [錯誤影響的資料流](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [JSON驗證結構](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)：驗證每個事件型別的要求裝載結構
>* [事件要求端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：媒體收集API端點參考
>* [工作階段要求端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)：在傳送事件之前建立工作階段
>* [播放器狀態追蹤](/help/use-cases/player-state-tracking/implementation-and-reporting.md)：狀態開始和狀態結束實作詳細資料
