---
title: 即時主要內容
description: 有關如何使用 Media SDK 追蹤即時內容的範例。
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 即時主要內容{#live-main-content}

## 藍本 {#scenario}

在此案例中，有一個沒有廣告的即時資產，在加入即時資料流後播放了 40 秒。

| 觸發 | 心率方法 | 網路呼叫 | 附註   |
|---|---|---|---|
| 使用者點按&#x200B;**[!UICONTROL 播放]** | `trackSessionStart` | Analytics 內容開始、心率內容開始 | 這可以是使用者點按&#x200B;**[!UICONTROL 播放]或自動播放事件。** |
| 媒體播放的第一個時間格。 | `trackPlay` | 心率內容播放 | 此方法會觸發計時器。只要播放繼續，便會每 10 秒傳送心率。 |
| 內容播放。 |  | 內容心率 |  |
| 工作階段已結束。 | `trackSessionEnd` |  | `SessionEnd` 表示檢視工作階段的結尾。即使使用者未持續使用到媒體完成，仍必須呼叫此 API。 |

## 參數 {#parameters}

您在 Adobe Analytics 內容開始呼叫上看到的許多相同值，也會在 Heartbeat 內容開始呼叫上看到。您也將看到 Adobe 用來在 Adobe Analytics 中填入各種「媒體」報表的許多其他參數。我們不會在此說明所有內容，只會說明真正重要的那些內容。

### 心率內容開始

| 參數 | 值 | 附註 |
|---|---|---|
| `s:sc:rsid` | &lt;Analytics 報表套裝 ID&gt; |  |
| `s:sc:tracking_serve` | &lt;您的 Analytics 追蹤伺服器 URL&gt; |  |
| `s:user:mid` | `s:user:mid` | 應該符合 Adobe Analytics 內容開始呼叫上的中間值 |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;您的媒體名稱&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | 可選 | 媒體上設定的自訂中繼資料 |

## 內容心率 {#content-heartbeats}

在媒體播放期間，對於主要內容，計時器將每隔 10 秒傳送一或多個心率 (或 Ping)；對於廣告，則為每秒。這些心率將包含關於播放、廣告、緩衝和一些其他項目的資訊。每個心率的確切內容不在本文件的範圍，要驗證的重要項目為，當播放繼續時會一致地觸發心率。

在內容心率中，尋找一些特定項目:

| 參數 | 值 | 附註 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;playhead position&gt; 例如 50、60、70 | 這應該反映播放點目前的位置。 |

## 心率內容完成{#heartbeat-content-complete}

在此案例中，不會有完成呼叫，因為即時資料流從不會結束。

## 播放點值設定

若為「即時」資料流，您必須將播放點設為節目開始的位移，這樣分析師就能在報表的 24 小時檢視內，判斷使用者在哪個時間點加入及離開「即時」資料流。

### 開始時

若為「即時」媒體，當使用者開始播放資料流時，您必須將 `l:event:playhead` 設為目前的位移 (以秒為單位)。與此相對的是，在 VOD 中，您會將播放點設為「0」。

例如，假設「即時」資料流事件在午夜開始並持續執行 24 小時 (`a.media.length=86400`; `l:asset:length=86400`)。接著，假設使用者在中午 12:00 開始播放該「即時」資料流。在此案例中，您應將 `l:event:playhead` 設為 43200 (12 小時進入資料流)。

### 暫停時

使用者暫停播放時，必須套用開始播放時所套用的同一個「即時播放點」邏輯。當使用者繼續播放「即時」資料流時，您必須將 `l:event:playhead` 值設為新的位移播放點位置，而&#x200B;_不是設為_&#x200B;使用者暫停「即時」資料流的時間點。

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
this._mediaHeartbeat.trackSessionEn