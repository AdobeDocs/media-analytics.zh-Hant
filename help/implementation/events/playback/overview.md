---
title: 追蹤播放
description: 瞭解播放事件以及如何實施播放、暫停、緩衝、Ping和位元速率變更追蹤。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 2%

---


# 追蹤播放

播放事件會在整個工作階段中追蹤媒體播放器中的狀態轉變。 它們構成事件串流的核心，並套用至任何內容型別。

## 播放器事件

| 播放器事件 | 動作 |
| --- | --- |
| 媒體播放或繼續 | 通話播放 |
| 媒體暫停 | 呼叫暫停開始 |
| 緩衝開始 | 呼叫緩衝開始 |
| 緩衝結束 | 通話播放 |
| 位元速率變更 | 呼叫位元速率變更 |
| 計時器觸發 | 呼叫Ping |

## 實作步驟

1. 當第一個內容畫面呈現時，在[工作階段開始](../session/session-start.md)之後，**呼叫[播放](play.md)**。 也可在暫停或緩衝停止後繼續播放時傳送播放。 沒有單獨的繼續事件。
1. 當使用者暫停播放時，**呼叫[暫停開始](pause-start.md)**。 繼續播放時傳送播放。
1. 播放器停止等候資料時，**呼叫[緩衝開始](buffer-start.md)**。 在XDM型API上，當您傳送下一個「播放」事件時會推斷緩衝結束。 在行動SDK上，解析緩衝時也明確地呼叫`BufferComplete`。
1. **在主要內容播放期間每10秒和廣告播放期間每1秒呼叫一次[Ping](ping.md)**。 Ping會保持工作階段進行中，並記錄播放點移動。 Mobile SDK會自動傳送ping；所有其他平台都必須手動傳送。
1. 當播放器交涉新的位元速率時，**呼叫[位元速率變更](bitrate-change.md)**。 包含目前的QoE資料 — 位元速率、每秒影格數、掉格數 — 讓後端可以計算[平均位元速率](/help/reporting/metrics/average-bitrate.md)和相關的品品質度。
