---
title: 從里程碑移轉至 Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: ht
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: ht
source-wordcount: '669'
ht-degree: 100%

---


# 從里程碑移轉至 Media Analytics {#migrating-from-milestone-to-media-analytics}

## 概述 {#overview}

「里程碑」和 Media Analytics 追蹤的影片測量核心概念相同，也就是擷取影片播放器事件，並對應至分析方法，同時擷取播放器中繼資料和值，將其對應至分析變數。Media Analytics 解決方案源自「里程碑」，因此許多方法和量度相同，但設定方式和程式碼則大有不同。應可更新播放器事件程式碼，顯示可能有新 Media Analytics 方法。如需實作 Media Analytics 的詳細資訊，請參閱 [SDK 概述](/help/sdk-implement/setup/setup-overview.md)和[追蹤概述](/help/sdk-implement/track-av-playback/track-core-overview.md)。

下列表格為「里程碑」解決方案和 Media Analytics 解決方案的對照表。

## 移轉指南 {#migration-guide}

### 變數參考資料

| 里程碑量度 | 變數類型 | Media Analytics 量度 |
| --- | --- | --- |
| 內容 | eVar <br>預設過期時間：造訪 | 內容 |
| 內容類型 | eVar <br>預設過期時間：頁面檢視 | 內容類型 |
| 內容逗留時間 | 事件<br>類型：計數器 | 內容逗留時間 |
| 影片起始 | 事件<br>類型：計數器 | 影片起始 |
| 影片完成 | 事件<br>類型：計數器 | 內容完成 |

### 媒體模組變數

| 里程碑 | 里程碑語法 | Media Analytics | Media Analytics 語法 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | 不適用 | 所有 Media Analytics 資料僅使用內容資料傳送。 |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 不適用 | Media Analytics 內容資料會自動填入保留的變數中。實作程式碼內不再需要對應 eVar、prop 和事件。客戶可使用處理規則，將內容資料對應至變數。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | 不適用 | 透過保留變數和處理規則對應後，此功能便不再需要。 |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | 不適用 | 透過保留變數和處理規則對應後，此功能便不再需要。 |

### 選擇性變數

| 里程碑 | 里程碑語法 | Media Analytics | Media Analytics 語法 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 不適用 | 不再提供預先建立的播放器對應。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 不適用 | 不再提供預先建立的播放器對應。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 不適用 | 「內容完成」僅支援 100% 進度標記。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 不適用 | 「內容完成」僅支援 100% 進度標記。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK 金鑰：playerName；<br>API 金鑰：media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 不適用 | Media Analytics 針對內容設為 10 秒，廣告則設為 1 秒。無其他可用選項。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 不適用 | Media Analytics 一律追蹤 10%、25%、50%、75%、95% 進度標記。。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 不適用 | Media Analytics 一律追蹤 10%、25%、50%、75%、95% 進度標記。。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 不適用 | 不再提供自動追蹤功能。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 不適用 | 不再提供自動追蹤功能。 |

### 廣告追蹤變數

| 里程碑 | 里程碑語法 | Media Analytics | Media Analytics 語法 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 不適用 | Media Analytics 針對內容設為 10 秒，廣告則設為 1 秒。無其他可用選項。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 不適用 | 廣告預設不提供進度標記。請使用計算量度建立廣告進度標記。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 不適用 | Media Analytics 針對廣告設定為 1 秒。無其他可用選項。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 不適用 | 不再提供自動追蹤功能。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 不適用 | 不再提供自動追蹤功能。 |

### 媒體模組方法

| 里程碑 | 里程碑語法 | Media Analytics | Media Analytics 語法 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`：(必填) 您希望在影片報表中顯示的名稱。 | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`：(必填) 影片長度 (以秒為單位)。 | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`：(必填) 觀看影片所使用的媒體播放器名稱，您希望影片報表中顯示的名稱。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`：(必填) 廣告名稱或 ID。 | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`：(必填) 廣告長度。 | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`：(必填) 觀看廣告所使用的媒體播放器名稱。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`：內嵌廣告所在主要內容的名稱或 ID。 | 不適用 | 自動繼承。 |
| parentPod | `parentPod`：主要內容中播放廣告的位置。 | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`：Pod 內播放廣告的位置。 | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`：此播放作業所採用的 CPM 或加密 CPM (首碼為「~」)。 | 不適用 | 預設為不提供 Media Analytics。 |
| Media.click | `s.Media.click(name, offset)` | 不適用 | 使用自訂連結分析呼叫追蹤點擊次數。 |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> 或 <br>trackEvent | `trackPause()`<br> 或 `trackEvent(`<br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)`<br> 或 <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | 使用自訂或標準中繼資料設定其他變數。 | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | 不適用 | 已自動設定追蹤呼叫頻率。 |
