---
seo-title: 從里程碑移轉至自訂連結
title: 從里程碑移轉至自訂連結
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 從里程碑移轉至自訂連結{#migrating-from-milestone-to-custom-link}

## 概述 {#section_xlc_fc2_dfb}

「里程碑」和「自訂連結」追蹤的視訊測量核心概念相同，也就是擷取視訊播放器事件，並對應至分析方法，同時擷取播放器中繼資料和值，將其對應至分析變數。「自訂連結」方法應視為同時減少及簡化實作和收集的資料。使用「自訂連結」解決方案，不會預先定義視訊測量的變數或方法，須完全自訂。應可更新播放器事件程式碼，以顯示可能有基本播放器事件 (如開始和結束) 的自訂連結追蹤呼叫。如需詳細資訊，請參閱[自訂連結實作指南](/help/measurement-options/cl-in-aa/cl-impl-guide.md)和[使用自訂連結程式碼的手動追蹤連結](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html)。

下列表格為「里程碑」解決方案和「自訂連結」解決方案的對照表。

## 移轉指南 {#section_btt_fc2_dfb}

### 視訊變數參考

<table>
<thead>
<tr>
<th><strong>里程碑量度</strong></th>
<th><strong>變數類型</strong></th>
<th><strong>自訂連結</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>內容</td>
<td>
<p>eVar</p>
<p>預設過期時間: 造訪</p>
</td>
<td>定義專屬 eVar</td>
</tr>
<tr>
<td>內容類型</td>
<td>
<p>eVar</p>
<p>預設過期時間: 頁面檢視</p>
</td>
<td>定義專屬 eVar</td>
</tr>
<tr>
<td>內容逗留時間</td>
<td>
<p>事件</p>
<p>類型: 計數器</p>
</td>
<td>定義專屬事件</td>
</tr>
<tr>
<td>視訊起始</td>
<td>
<p>事件</p>
<p>類型: 計數器</p>
</td>
<td>定義專屬事件</td>
</tr>
<tr>
<td>視訊完成</td>
<td>
<p>事件</p>
<p>類型: 計數器</p>
</td>
<td>定義專屬事件</td>
</tr>
</tbody>
</table>

### 媒體模組變數

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>自訂連結
</th>
<th>自訂連結語法
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name';
s.contextData[『video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name":    "eVar2,prop2"、"a.media.segment":    "eVar3"、"a.contentType":    "eVar1"、"a.media.timePlayed":    "event3"、"a.media.view":    "event1"、"a.media.segmentView":    "event2"、"a.media.complete":    "event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>不適用
</td>
<td>目前已透過處理規則，將內容資料對應至 eVar、prop 和事件。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData。
       video.name、contextData。
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑語法
</th>
<th>自訂連結
</th>
<th>自訂連結語法
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name';
s.contextData[『video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view", "a.media.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>不適用
</td>
<td>目前已透過處理規則，將內容資料對應至 eVar、prop 和事件。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData。
       video.name、contextData。
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
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
<th>自訂連結
</th>
<th>自訂連結語法
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
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>不適用
</td>
<td>無法使用
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
在連結呼叫設定 eVar 或內容資料變數
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer名稱";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>不適用
</td>
<td>無法使用
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
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones = true;
</pre>
</td>
<td>不適用
</td>
<td>無法使用
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
<th>自訂連結
</th>
<th>自訂連結語法
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones = true;
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones = true;
</pre>
</td>
<td>不適用
</td>
<td>無法使用
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
<th>自訂連結
</th>
<th>自訂連結語法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';s.linkTrackEvents = 'event2';s.prop10 = mediaName;s.eVar10 = mediaName;s.eVar12 = "video";s.eVar15 = mediaPlayerName;s.events = 'event2';s.contextData['video.name'] = mediaName;s.contextData['video.view'] = 'true';s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b></b> mediaName:（必要）視訊的名稱，如您所希望的顯示在視訊報表中。</td>
<td>在連結呼叫設定 eVar 或內容資料變數</td>
<td>
<pre>
s.prop10 = mediaName;s.eVar10 = mediaName;s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b></b> mediaLength:（必要）視訊長度（以秒為單位）。
</td>
<td>
在連結呼叫設定 eVar 或內容資料變數
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b></b> mediaPlayerName:（必要）用於檢視視訊的媒體播放器名稱，如您想要它顯示在視訊報表中。
</td>
<td>
在連結呼叫設定 eVar 或內容資料變數
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer名稱";
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
<td>不適用
</td>
<td>無法使用</td>
</tr>
<tr>
<td>name</td>
<td><b></b> 名稱：（必要）廣告的名稱或ID。</td>
<td>不適用</td>
<td>無法使用</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b></b> 長度：（必要）廣告的長度。
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b></b> playerName:（必要）用於檢視廣告的媒體播放器名稱。
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> 內嵌廣告所在主要內容的名稱或 ID。
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> 主要內容中播放廣告的位置。
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> Pod 內播放廣告的位置。
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> 套至用此播放的 CPM 或加密的 CPM (首碼為 "~")。
</td>
<td>不適用
</td>
<td>無法使用
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
<td>
<pre>
s.tl()
</pre>
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
<td>不適用
</td>
<td>無法使用
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData。
       video.name、contextData。
       video.complete';s.linkTrackEvents = 'event3';s.prop10 = mediaName;s.eVar10 = mediaName;s.eVar12 = "video";s.eVar15 = mediaPlayerName;s.events = 'event3';s.contextData['video.name'] = mediaName;s.contextData['video.complete'] = 'true';s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment, segmentLength)
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>不適用 
</td>
<td>無法使用
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
在連結呼叫設定 eVar 或內容資料變數
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData。
       video.name、contextData。
       video.view';s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>不適用
</td>
<td>無法使用
</td>
</tr>
</tbody>
</table>

