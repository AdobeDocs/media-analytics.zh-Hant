---
title: 即時主要內容
description: 如何使用Media SDK追蹤即時內容的範例。
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 即時主要內容{#live-main-content}

## 藍本 {#scenario}

在此案例中，有一個沒有廣告的即時資產，在加入即時資料流後播放了 40 秒。

| 觸發 | 心率方法 | 網路呼叫 | 附註   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics 內容開始、心率內容開始 | 這可以是使用者點按&#x200B;**[!UICONTROL 播放]或自動播放事件。** |
| 媒體播放的第一個畫格。 | `trackPlay` | 心率內容播放 | 此方法會觸發計時器。只要播放繼續，便會每 10 秒傳送心率。 |
| 內容播放。 |  | 內容心率 |  |
| 工作階段已結束。 | `trackSessionEnd` |  | `SessionEnd` 表示檢視工作階段的結尾。即使使用者未使用媒體完成，也必須呼叫此API。 |

## 參數 {#parameters}

您在 Adobe Analytics 內容開始呼叫上看到的許多相同值，也會在 Heartbeat 內容開始呼叫上看到。您也會看到Adobe在Adobe Analytics中用來填入各種媒體報表的許多其他參數。 我們不會在此說明所有內容，只會說明真正重要的那些內容。

### 心率內容開始

| 參數 | 值 | 附註 |
|---|---|---|
| `s:sc:rsid` | &lt;Your Adobe Report Suite ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Your Analytics Tracking Server URL&gt; |  |
| `s:user:mid` | `s:user:mid` | 應該符合 Adobe Analytics 內容開始呼叫上的中間值 |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;您的媒體名稱&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | 可選 | 媒體上的自訂中繼資料集 |

## 內容心率 {#content-heartbeats}

在媒體播放期間，計時器會每10秒傳送一或多個心率（或ping），以用於主要內容，而每秒傳送一個或多個廣告。 這些心率將包含關於播放、廣告、緩衝和一些其他項目的資訊。每個心率的確切內容不在本文件的範圍，要驗證的重要項目為，當播放繼續時會一致地觸發心率。

在內容心率中，尋找一些特定項目:

| 參數 | 值 | 附註 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;playhead position&gt; 例如 50、60、70 | 這應該反映播放點目前的位置。 |

## 心率內容完成 {#heartbeat-content-complete}

在此情景中，不會有完整呼叫，因為即時串流從未完成。

## 播放頭值設定

對於LIVE串流，您必須將播放磁頭設為與程式設計開始時的偏移值，如此，在報告中，分析師就可判斷使用者在24小時檢視內加入和離開LIVE串流的時間點。

### 開始時

對於即時媒體，當使用者開始播放串流時，您必須在數 `l:event:playhead` 秒內設定目前的偏移。 這與VOD不同，您可將播放頭設為"0"。

例如，假設一個即時串流活動從午夜開始，持續24小時(`a.media.length=86400`; `l:asset:length=86400`)。 然後，假設使用者在下午12:00開始播放該即時串流。 在此案例中，您應設 `l:event:playhead` 定為43200（在串流中為12小時）。

### 暫停時

當使用者暫停播放時，必須套用在播放開始時套用的相同「即時播放磁頭」邏輯。 當使用者返回播放LIVE串流時，您必須將 `l:event:playhead` 值設定為新的偏移播放頭位置， __ 而非使用者暫停LIVE串流的點。

## 程式碼範例 {#sample-code}

![](assets/live-content-playback.png)

### Android

以下是預期的 API 呼叫順序:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS 應用程式

以下是預期的 API 呼叫順序:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

以下是預期的 API 呼叫順序:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

