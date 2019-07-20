---
seo-title: 從里程碑移轉至 Media Analytics
title: 從里程碑移轉至 Media Analytics
uuid: fdc96146-af63-48ce-b938-c0 ca77029277
translation-type: tm+mt
source-git-commit: 27740fc1753e8ac9cf5a4b240a56b1c2dd567010

---


# 從里程碑移轉至 Media Analytics {#migrating-from-milestone-to-media-analytics}

## 概述 {#section_ihl_nbz_cfb}

「里程碑」和 Media Analytics 追蹤的視訊測量核心概念相同，也就是擷取視訊播放器事件，並對應至分析方法，同時擷取播放器中繼資料和值，將其對應至分析變數。Media Analytics 解決方案源自「里程碑」，因此許多方法和量度相同，但設定方式和程式碼則大有不同。應可更新播放器事件程式碼，顯示可能有新 Media Analytics 方法。See [SDK Overview](../../sdk-implement/setup/setup-overview.md) and [Tracking Overview](../../sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

下列表格為「里程碑」解決方案和 Media Analytics 解決方案的對照表。

## 移轉指南 {#section_iyb_pbz_cfb}

### 變數參考

| 里程碑量度 | 變數類型 | Media Analytics 量度 |
| --- | --- | --- |
| 內容 | eVar<br/><br/>Default expiration: Visit | 內容 |
| 內容類型 | eVar<br/><br/> Default expiration: Page view | 內容類型 |
| 內容逗留時間 | Event<br/><br/> Type: Counter | 內容逗留時間 |
| 視訊起始 | Event<br/><br/> Type: Counter | 視訊起始 |
| 視訊完成 | 事件<br/><br/> 類型: 計數器 | 內容完成 |

### 媒體模組變數

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 語法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>不適用
</td>
<td>所有 Media Analytics 資料僅使用內容資料傳送。
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s. Media. contextDataMapping={a.
 media. name」：「eVar2、prop2」、「a.
 media. segment」：「eVar3」，「a.
 contentType」：「eVar1」，「a.
 media. TimePlayed」：「event3」，「a.
 media. view」：「event1」，「a.
 media. segmentView」：「event2」，「a.
 media. complete」：「event7」，「a.
 media. milestones」：{25：「event4」，50：「event5」，75：「event6」}}；
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 內容資料會自動填入保留的變數。實作程式碼內不再須對應 eVar、prop 和事件。客戶可使用處理規則，將內容資料對應至變數。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s. Media. trackVars=
「events、prop2、eVar1、eVar2、eVar3」；
</pre>
</td>
<td>不適用
</td>
<td>透過保留變數和處理規則對應後便不再需要。
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackEvents=
「event1、event2、event3、event4、event5、event6、event7」
</pre>
</td>
<td>不適用
</td>
<td>透過保留變數和處理規則對應後便不再需要。
</td>
</tr>
</tbody>
</table>

### 選擇性變數

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 語法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>不適用
</td>
<td>不再提供預先建立的播放器對應。
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams=
 true
</pre>
</td>
<td>不適用
</td>
<td>不再提供預先建立的播放器對應。
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeBycloseOffset=
 true
</pre>
</td>
<td>不適用
</td>
<td>「內容結束」僅支援 100% 進度標記。
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeLoseOffsetThreshold=1
</pre>
</td>
<td>不適用
</td>
<td>「內容結束」僅支援 100% 進度標記。
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Custom Player Name"
</pre>
</td>
<td>
SDK金鑰：playerName；
API金鑰：media. playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds=15
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 針對內容設定 10 秒，廣告為 1 秒。無其他可用選項。
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones=「25,50,75」；
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 一律追蹤 10%、25%、50%、75%、95% 進度標記。
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones=「20,40,60」；
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 一律追蹤 10%、25%、50%、75%、95% 進度標記。
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>不適用
</td>
<td>無法再使用自動追蹤
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones=
 true；
</pre>
</td>
<td>不適用
</td>
<td>無法再使用自動追蹤
</td>
</tr>
</tbody>
</table>

### 廣告追蹤變數

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 語法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds=15
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 針對內容設定 10 秒，廣告為 1 秒。無其他可用選項。
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones=「25,50,75」；
</pre>
</td>
<td>不適用
</td>
<td>廣告預設不提供進度標記。請使用計算量度建立廣告進度標記。
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adtrackOffsetMilestones=「20,40,60」；
</pre>
</td>
<td>不適用
</td>
<td>Media Analytics 針對廣告設定 1 秒。無其他可用選項。
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adsegmentBymilestones=
 true；
</pre>
</td>
<td>不適用
</td>
<td>無法再使用自動追蹤
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adsegmentByOffsetMilestones=
 true；
</pre>
</td>
<td>不適用
</td>
<td>無法再使用自動追蹤
</td>
</tr>
</tbody>
</table>

### 媒體模組方法

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 語法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(MediaObject，
contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName-(必要)視訊的名稱，您希望它顯示在視訊報表中。
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createEdiaObject(名稱，
MediaAp，
length，
StreamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength-(必要)視訊長度在秒內。
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createEdiaObject(名稱，
MediaAp，
length，
StreamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName-(必要)用於檢視視訊的媒體播放器名稱，如您希望它顯示在視訊報表中。
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>
<pre>
TrackEvent
</pre>
</td>
<td>
<pre>
MediaHeartbeat. trackEvent(MediaHeartbeat)。
 事件.
    AdBrestart、
AdBreakObject)；
…
trackEvent(MediaHeartbeat)
 事件.
    AdStart、
AdObject、
adCustomMetadata)；
</pre>
</td>
</tr>
<tr>
<td>
name-(必要)廣告的名稱或ID。
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
CreateAdject(名稱，
AdID，
位置、
長度)
</pre>
</td>
</tr>
<tr>
<td>
長度(必要)廣告長度。
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
CreateAdject(名稱，
AdID，
位置、
長度)
</pre>
</td>
</tr>
<tr>
<td>
playerName-(必要)用於檢視廣告的媒體播放器名稱。
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName-內嵌廣告之主要內容的名稱或ID。
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>不適用
</td>
<td>自動繼承
</td>
</tr>
<tr>
<td>
parentPod-主要內容中播放廣告的位置。
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
CreateAdbreakObject(名稱，
位置、
startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPointPosition- pod在播放廣告位置中的位置。
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
CreateAdject(名稱，
AdID，
位置、
長度)
</pre>
</td>
</tr>
<tr>
<td>
CPM，CPM或加密的CPM(加上「~」)，適用於此播放。
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>不適用
</td>
<td>在Media Analytics中預設無法使用
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>不適用
</td>
<td>使用自訂連結分析呼叫追蹤點擊次數
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment, segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> 或  
<pre>
TrackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
或 
<pre>
TrackEvent(MediaHeartbeat)。
 事件.
  SeekStart)
</pre> 或 
<pre>
TrackEvent(MediaHeartbeat)。
 事件.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>使用自訂或標準中繼資料設定其他變數
</td>
<td>
<pre>
var customVideoMetadata={IsUserLoggedIn：
「false」，TVstation：
「範例電視節目表」，程式設計人員：
「範例程式設計人員」}；
…
var StandardVideoMetadata
={}；
StandardVideoMetadata[mediaHeartbeat.
 VideoMetadataKeys.
   ESEDE]=
「範例Epode」；
StandardVideoMetadata[mediaHeartbeat.
 VideoMetadataKeys.
   Show]=「Sample Show」；
…
MediaObject. setValue(MediaHeartbeat)
 MediaObjectKey。
 standardVideoMetadata，
standardVideoMetadata)；
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>不適用
</td>
<td>已自動設定追蹤呼叫頻率。
</td>
</tr>
</tbody>
</table>

