---
title: 從里程碑移轉至自訂連結
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: ht
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: ht
source-wordcount: '576'
ht-degree: 100%

---


# 從里程碑移轉至自訂連結{#migrating-from-milestone-to-custom-link}

## 概述 {#overview}

「里程碑」和「自訂連結」追蹤的影片測量核心概念相同，也就是擷取影片播放器事件，並對應至分析方法，同時擷取播放器中繼資料和值，將其對應至分析變數。「自訂連結」方法應視為同時減少及簡化實作和收集的資料。使用「自訂連結」解決方案，不會預先定義影片測量的變數或方法，須完全自訂。應可更新播放器事件程式碼，以顯示可能有基本播放器事件 (如開始和結束) 的自訂連結追蹤呼叫。如需詳細資訊，請參閱[自訂連結實作指南](/help/measurement-options/cl-in-aa/cl-impl-guide.md)。

下表為「里程碑」解決方案和「自訂連結」解決方案的對照表。

## 移轉指南 {#migration-guide}

### 影片變數參考

| 里程碑量度 | 變數類型 | 自訂連結 |
| --- | --- | --- |
| 內容 | eVar <br>預設過期時間：造訪 | 定義專屬 eVar。 |
| 內容類型 | eVar <br>預設過期時間：頁面檢視 | 定義專屬 eVar。 |
| 內容逗留時間 | 事件<br>類型：計數器 | 定義專屬事件。 |
| 影片起始 | 事件<br>類型：計數器 | 定義專屬事件。 |
| 影片完成 | 事件<br>類型：計數器 | 定義專屬事件。 |

### 媒體模組變數

| 里程碑 | 里程碑語法 | 自訂連結 | 自訂連結語法 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 不適用 | 目前已透過處理規則，將內容資料對應至 eVar、prop 和事件。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### 選擇性變數

| 里程碑 | 里程碑語法 | 自訂連結 | 自訂連結語法 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 不適用 | 無法使用。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 不適用 | 無法使用。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 不適用 | 無法使用。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 不適用 | 無法使用。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | 在連結呼叫設定 eVar 或內容資料變數。 | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 不適用 | 無法使用。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 不適用 | 無法使用。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 不適用 | 無法使用。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 不適用 | 無法使用。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 不適用 | 無法使用。 |

### 廣告追蹤變數

| 里程碑 | 里程碑語法 | 自訂連結 | 自訂連結語法 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 不適用 | 無法使用。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 不適用 | 無法使用。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 不適用 | 無法使用。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 不適用 | 無法使用。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 不適用 | 無法使用。 |

### 媒體模組方法

| 里程碑 | 里程碑語法 | 自訂連結 | 自訂連結語法 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`：(必填) 您希望在影片報表中顯示的名稱。 | 在連結呼叫設定 eVar 或內容資料變數。 | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`：(必填) 影片長度 (以秒為單位)。 | 在連結呼叫設定 eVar 或內容資料變數。 | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`：(必填) 觀看影片所使用的媒體播放器名稱，您希望影片報表中顯示的名稱。 | 在連結呼叫設定 eVar 或內容資料變數。 | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | 不適用 | 無法使用。 |
| name | `name`：(必填) 廣告名稱或 ID。 | 不適用 | 無法使用。 |
| length | `length`：(必填) 廣告長度。 | 不適用 | 無法使用。 |
| playerName | `playerName`：(必填) 觀看廣告所使用的媒體播放器名稱。 | 不適用 | 無法使用。 |
| parentName | `parentName`：內嵌廣告所在主要內容的名稱或 ID。 | 不適用 | 無法使用。 |
| parentPod | `parentPod`：主要內容中播放廣告的位置。 | 不適用 | 無法使用。 |
| parentPodPosition | `parentPodPosition`：Pod 內播放廣告的位置。 | 不適用 | 無法使用。 |
| CPM | `CPM`：此播放作業所採用的 CPM 或加密 CPM (首碼為「~」)。 | 不適用 | 無法使用。 |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | 使用自訂連結分析呼叫追蹤點擊次數。 |
| Media.close | `s.Media.close(mediaName)` | 不適用 | 無法使用。 |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | 不適用 | 無法使用。 |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | 不適用 | 無法使用。 |
| Media.monitor | `s.Media.monitor(s, media)` | 在連結呼叫設定 eVar 或內容資料變數。 | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | 不適用 | 無法使用。 |
