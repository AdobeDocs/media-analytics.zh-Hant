---
seo-title: 即時主要內容
title: 即時主要內容
uuid: e92e99f4-c395-48aa-8a30-cbdd2 f5 fc07 c
translation-type: tm+mt
source-git-commit: 9dbd621e10ba198b9331e5a7579fcbd3b6173ecd

---


# 即時主要內容{#live-main-content}

## 藍本 {#section_13BD203CBF7546D2A6AD0129B1EEB735}

在此案例中，有一個沒有廣告的即時資產，在加入即時資料流後播放了 40 秒。

| 觸發 | 心率方法 | 網路呼叫 | 附註   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics 內容開始、心率內容開始 | 這可以是使用者點按&#x200B;**[!UICONTROL 播放]或自動播放事件。** |
| 媒體播放的第一個畫格。 | `trackPlay` | 心率內容播放 | 此方法會觸發計時器。只要播放繼續，便會每 10 秒傳送心率。 |
| 內容播放。 |  | 內容心率 |  |
| 工作階段已結束。 | `trackSessionEnd` |  | `SessionEnd` 表示檢視工作階段的結尾。即使使用者不使用媒體，也必須呼叫此API。 |

## 參數 {#section_D52B325B99DA42108EF560873907E02C}

您在 Adobe Analytics 內容開始呼叫上看到的許多相同值，也會在 Heartbeat 內容開始呼叫上看到。您也會看到Adobe用來填入Adobe Analytics中各種媒體報表的其他參數。我們不會在此說明所有內容，只會說明真正重要的那些內容。

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
| `s:meta:*` | 可選 | 媒體上設定的自訂中繼資料 |

## 內容心率 {#section_7B387303851A43E5993F937AE2B146FE}

在媒體播放期間，會有計時器每10秒傳送一或多個心率。這些心率將包含關於播放、廣告、緩衝和一些其他項目的資訊。每個心率的確切內容不在本文件的範圍，要驗證的重要項目為，當播放繼續時會一致地觸發心率。

在內容心率中，尋找一些特定項目:

| 參數 | 值 | 附註 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;playhead position&gt; 例如 50、60、70 | 這應該反映播放點目前的位置。 |

## 心率內容完成 {#section_2CA970213AF2457195901A93FC9D4D0D}

這個情況下不會有完整的呼叫，因為即時串流從未完成。

## 播放磁頭值設定

對於即時串流，您需要將播放磁頭設定為從程式設計開始時的偏移，如此在報告中，分析人員可以決定在24小時檢視內，使用者加入並離開即時串流的時間。

### at Start

For LIVE media, when a user starts playing the stream, you need to set `l:event:playhead` to the current offset, in seconds. 這與VOD相反，您可將播放磁頭設為「0」。

For example, say a LIVE streaming event starts at midnight and runs for 24 hours (`a.media.length=86400`; `l:asset:length=86400`). 然後，假設使用者在下午12：00開始播放該即時串流。In this scenario, you should set `l:event:playhead` to 43200 (12 hours into the stream).

### 暫停

在播放開始時套用的相同「live Playhead」邏輯，必須在使用者暫停播放時套用。When the user returns to playing the LIVE stream, you must set the `l:event:playhead` value to the new offset playhead position, _not_ to the point where the user paused the LIVE stream.

## 程式碼範例 {#section_vct_j2j_x2b}

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

