---
title: 追蹤內容播放
description: 瞭解如何追蹤核心播放，包括追蹤媒體載入、媒體開始、媒體暫停和媒體完成。
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# 追蹤內容播放

核心播放追蹤涵蓋媒體載入、開始、暫停、繼續、完成和工作階段結束。 緩衝和搜尋追蹤雖然並非為強制性，但也是完整播放實作的核心元件。

## 播放器事件

| 播放器事件 | 動作 |
| --- | --- |
| 媒體載入 | 建立媒體物件；呼叫SessionStart |
| 媒體開始 | 通話播放 |
| 暫停 | 呼叫PauseStart |
| 從暫停繼續 | 通話播放 |
| 媒體完成 | 呼叫Sessioncomplete |
| 媒體中止/解除安裝 | 呼叫工作階段結束 |
| 緩衝開始 | 呼叫Bufferstart |
| 緩衝結束 | 通話播放（繼續） |
| 搜尋開始 | 呼叫SeekStart |
| 搜尋結束 | 呼叫SeekComplete；然後呼叫Play |

## 實作步驟

1. **識別使用者何時觸發播放** （使用者點按播放或自動播放觸發）。 建立具有內容名稱、ID、長度、資料流型別和媒體型別的媒體物件。 如需欄位定義，請參閱[內容名稱](/help/implementation/variables/core/content-name.md)、[內容識別碼](/help/implementation/variables/core/content-id.md)、[內容長度](/help/implementation/variables/core/content-length.md)、[資料流型別](/help/implementation/variables/core/stream-type.md)以及[內容型別](/help/implementation/variables/core/content-type.md)。
1. **可選擇附加中繼資料** — 標準中繼資料（節目、季度、集數等） 和自訂內容資料變數。 如需標準中繼資料金鑰參考，請參閱[節目](/help/implementation/variables/standard-metadata/show.md)、[季](/help/implementation/variables/standard-metadata/season.md)、[集數](/help/implementation/variables/standard-metadata/episode.md)、[型別](/help/implementation/variables/standard-metadata/genre.md)和[網路](/help/implementation/variables/standard-metadata/network.md)。
1. **呼叫[工作階段開始](/help/implementation/events/session/session-start.md)**&#x200B;以開始追蹤工作階段。 這會載入資料和中繼資料，並開始QoS測量的開始時間。 SessionStart會追蹤要播放的&#x200B;*意圖*，而不是第一個影格。
1. 當熒幕上呈現內容的第一個畫面格時，**撥打[播放](/help/implementation/events/playback/play.md)**。
1. 播放器暫停時，**呼叫[暫停開始](/help/implementation/events/playback/pause-start.md)**。 繼續播放時再次呼叫播放。 沒有單獨的繼續事件。
1. 當檢視器到達內容結尾時，**呼叫[工作階段完成](/help/implementation/events/session/session-complete.md)**。
1. 播放器解除安裝或檢視器放棄內容而未到達結尾時，**呼叫[工作階段結束](/help/implementation/events/session/session-end.md)**。 SessionEnd會立即關閉工作階段；之後將無法追蹤其他事件。

>[!IMPORTANT]
>
>`SessionEnd` 會標記追蹤工作階段的結尾。 如果成功觀看工作階段至完成，請在`SessionEnd`之前呼叫`SessionComplete`。 在`SessionEnd`之後會忽略任何其他追蹤呼叫，新工作階段的`SessionStart`除外。

## 核心播放

下列範例顯示完整的作業階段流程 — 從作業階段開始到內容完成和工作階段結束。

如需依平台的實作詳細資料，請參閱[工作階段開始](/help/implementation/events/session/session-start.md)、[播放](/help/implementation/events/playback/play.md)、[暫停開始](/help/implementation/events/playback/pause-start.md)、[工作階段完成](/help/implementation/events/session/session-complete.md)以及[工作階段結束](/help/implementation/events/session/session-end.md)。

## 緩衝

緩衝開始訊號表示播放器正在等待資料。 在BufferStart （XDM型API）之後傳送播放事件時推斷為緩衝結束。 在行動SDK上，也需明確呼叫BufferComplete。

如需實作詳細資料，請參閱[緩衝開始](/help/implementation/events/playback/buffer-start.md)。

## 搜尋

搜尋開始訊號表示檢視器正在拖曳。 搜尋結束之後接著播放，以繼續播放內容。

如需實作詳細資料，請參閱[暫停開始](/help/implementation/events/playback/pause-start.md) （搜尋開始）和[播放](/help/implementation/events/playback/play.md) （搜尋結束）。

## 處理應用程式中斷

媒體應用程式中的播放作業可能會因為多種原因而中斷，例如使用者按下暫停、應用程式進入背景、來電等。 無論原因為何，追蹤指示保持不變：

1. 當應用程式中斷（進入背景、媒體暫停等）時，呼叫&#x200B;**PauseStart**。
1. 當應用程式返回前景及/或媒體恢復播放時，呼叫&#x200B;**播放**。

>[!NOTE]
>
>應用程式從背景返回時，請勿呼叫SessionStart。 呼叫SessionStart會導致截至當時為止的播放不計入播放時間總計，而且先前的進度標籤、區段和章節邊界會遺失。

**暫停的工作階段應該何時結束？** 如果應用程式不允許背景播放，請立即呼叫PauseStart ，然後在背景執行約一分鐘後呼叫SessionEnd 。 應用程式無法從背景繼續傳送暫停Ping，而且讓工作階段無限期開啟會造成不良體驗。 如果應用程式不支援背景播放（音訊應用程式、視訊播客應用程式），請在背景中繼續傳送Ping。

**在漫長的背景期間之後重新啟動：**&#x200B;如果應用程式在背景執行的時間夠長，工作階段已過期（30分鐘未活動），請呼叫SessionEnd以完全關閉任何延遲的工作階段，然後在檢視器返回時呼叫SessionStart以開始新的工作階段。

## 繼續非作用中工作階段

如果在10分鐘內未收到任何事件，或播放點在30分鐘內未移動，工作階段會自動過期。 如果使用者在工作階段過期之後回訪，請再次呼叫SessionStart以開啟新的工作階段。

**跨裝置繼續（跨裝置移交）：**&#x200B;當檢視器在裝置之間傳輸播放時（例如，從電話轉換到電視），請使用繼續旗標在Analytics報表中將工作階段拼接在一起：

1. 在&#x200B;**來源裝置**&#x200B;上，當檢視器啟動轉換時，請呼叫SessionEnd。 不要呼叫SessionComplete — 內容尚未完成。
1. 在&#x200B;**目的地裝置**&#x200B;上，呼叫SessionStart並將恢復旗標設為`true`，並從來源裝置傳遞相同的內容中繼資料和播放點位置。

設定繼續旗標會使Analytics遞增[內容繼續](/help/reporting/metrics/content-resumes.md)，而非[媒體開始](/help/reporting/metrics/media-starts.md)，做為切換的第二個階段。

**手動繼續先前關閉的工作階段：**&#x200B;如果應用程式儲存使用者資料並且可以繼續先前關閉的工作階段，請在工作階段開始時設定繼續旗標。 如需所有平台的實作詳細資料，請參閱[工作階段開始](/help/implementation/events/session/session-start.md#resuming-a-session)。
