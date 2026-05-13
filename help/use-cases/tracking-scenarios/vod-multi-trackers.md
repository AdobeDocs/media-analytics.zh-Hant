---
title: 多個 VOD 追蹤器並行
description: 檢視如何使用多個追蹤器並行追蹤 VOD 的範例。
uuid: 6e25dd92-522f-455c-8e71-99d71d352e06
exl-id: 318beba8-bb26-4cec-81d7-c6fc446ec7b4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/wMYVK9HfRpdPfz4aiFEKOaTDHj548se9hySTd3ux9g8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 245
ht-degree: 100%

---

# 多個 VOD 追蹤器並行{#vod-multiple-trackers-in-parallel}

## 情境 {#scenario}

此情境中，有兩個工作階段並行執行兩個不同的媒體，並使用兩個不同的 `MediaHeartbeat` 例項。

除了有兩個工作階段並行執行兩個不同的媒體以外，此情境等同於[沒有廣告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)情境。 每一個工作階段會使用不同的 `MediaHeartbeat` 例項。

除非另有指定，否則網路呼叫與[沒有廣告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)情境相同。

## 參數 {#parameters}

### 心率工作階段

| 參數 | 值 | 附註   |
|---|---|---|
| `s:event:sid` | 唯一工作階段 ID | 呼叫 `trackSessionEnd` 方法之前，存在於所有心率網路呼叫的唯一工作階段 ID。 |

## 程式碼範例 {#sample-code}

![](assets/multi-sessions-in-parallel.png)

### Android

```java
public class MediaAnalyticsProvider implements MediaHeartbeatDelegate { 
  private MediaPlayer _player; 
  private MediaHeartbeat _heartbeat; 

  public MediaAnalyticsProvider(MediaPlayer player) { 
      if (player == null) { 
          throw new IllegalArgumentException("Player reference cannot be null."); 

      } 
      _player = player;  
      _player.addObserver(this); 

      // Media Heartbeat initialization 
      MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
      config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
      config.channel = HEARTBEAT_CHANNEL; 
      config.appVersion = HEARTBEAT_SDK; 
      config.ovp = HEARTBEAT_OVP; 
      config.playerName = PLAYER_NAME; 
      config.ssl = false; 
      config.debugLogging = true;  

      _heartbeat = new MediaHeartbeat(this, config); 
  } 

  @Override 
  public MediaObject getQoSObject() { 
      return MediaHeartbeat.createQoSObject(BITRATE,  
                                            STARTUP_TIME,  
                                            FPS,  
                                            DROPPED_FRAMES); 
  } 

  @Override 
  public Double getCurrentPlaybackTime() { 
      return _player.getCurrentPlaybackTime(); 
  } 
} 
```

```java
@Override 
protected void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.activity_main); 

  // Bootstrap the AdobeMobile library.  
  Config.setContext(this.getApplicationContext()); 

  // Create first MediaPlayer instance.  
  _player1 = new MediaPlayer(); 

  // Create first MediaAnalyticsProvider instance and 
  // attach it to the MediaPlayer instance.  
  _analyticsProvider1 = new MediaAnalyticsProvider(_player1); 

  // Load the main media content.  
  Uri uri =  
    Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.media1);  
  _player1.loadContent(uri); 

  // Create second MediaPlayer instance.  
  _player2 = new MediaPlayer(); 

  // Create second MediaAnalyticsProvider instance and 
  // attach it to the MediaPlayer instance.  
  _analyticsProvider2 = new MediaAnalyticsProvider(_player2); 

  // Load the main media content.  
  Uri uri =  
    Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.media2);  
  _player2.loadContent(uri); 
} 
```

`MediaAnalyticsProvider` 和 `MediaHeartbeat` 這兩個例項追蹤個別的工作階段，每一個都具有其自己的唯一工作階段 ID。 Charles 除錯工具或除錯記錄中的兩個工作階段，可透過使用工作階段 ID 值來加以識別。 如要在 Android 上顯示此情境，請設定下列程式碼：

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID, 
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
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

// 3. Call trackComplete() when the playback reaches the end, i.e., when the 
//    media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the media to completion. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

```
@interface MediaAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 

@end    

@implementation { 
  MediaPlayer *_player; 
} 

- (instancetype)initWithPlayer:(AVPlayer *)player { 
  if (self = [super init]) { 
      _player = player; 

      ADBMediaHeartbeatConfig *config =  
        [[ADBMediaHeartbeatConfig alloc] init]; 
      config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
      config.channel = HEARTBEAT_CHANNEL; 
      config.appVersion = HEARTBEAT_SDK_VERSION; 
      config.playerName = PLAYER_NAME; 
      config.ssl = SSL_SETTING; 
      config.debugLogging = DEBUG_SETTING; 

      ADBMediaHeartbeatConfig *config =  
        [[ADBMediaHeartbeatConfig alloc] init];       
      _mediaHeartbeat =  
        [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
        
      [self setupPlayerNotifications]; 
  } 

  return self; 
} 

- (ADBMediaObject *)getQoSInfo { 
  return [ADBMediaHeartbeat createQoSObjectWithBitrate:CURRENT_BITRATE_VALUE  
                            startupTime:CALCULATED_STARTED_TIME  
                            fps:CALCULATED_FPS  
                            droppedFrames:DROPPED_FRAMES_COUNT]; 
} 

- (NSTimeInterval)getCurrentPlaybackTime { 
  return CMTimeGetSeconds(_player.currentTime); 
} 

@end 

- (void)viewDidAppear:(BOOL)animated { 
  [super viewDidAppear:animated]; 
  [ADBMobile setDebugLogging:YES]; 

  // Setup the first media player 
  NSURL *streamUrl = [NSURL URLWithString:CONTENT_URL_1]; 

  if (!self.mediaPlayer1) { 
      self.mediaPlayer1 = [[MediaPlayer alloc] initWithContentURL:streamUrl]; 
      //setup player 
  } 

  // Create the MediaAnalyticsProvider instance and attach it to the first  
  // MediaPlayer instance. 
  if (!self.mediaAnalyticsProvider1) { 
      self.mediaAnalyticsProvider1 =  
        [[MediaAnalyticsProvider alloc] initWithPlayerDelegate:self.mediaPlayer1]; 
  } 

  // Setup the second media player 
  NSURL *streamUrl2 = [NSURL URLWithString:CONTENT_URL_2]; 

  if (!self.mediaPlayer2) { 
      self.mediaPlayer2 = [[MediaPlayer alloc] initWithContentURL:streamUrl2]; 
      //setup player 
  } 

  // Create the MediaAnalyticsProvider instance and attach it to the second  
  // MediaPlayer instance. 
  if (!self.mediaAnalyticsProvider2) { 
      self.mediaAnalyticsProvider2 =  
        [[MediaAnalyticsProvider alloc] initWithPlayerDelegate:self.mediaPlayer2]; 
  } 
} 
```

```
- (void)viewDidAppear:(BOOL)animated { 
  [super viewDidAppear:animated]; 
  [ADBMobile setDebugLogging:YES]; 

  // Setup the first media player 
  NSURL *streamUrl = [NSURL URLWithString:CONTENT_URL_1]; 

  if (!self.mediaPlayer1) { 
      self.mediaPlayer1 = [[MediaPlayer alloc] initWithContentURL:streamUrl]; 
      //setup player 
  } 

  // Create the MediaAnalyticsProvider instance and attach it to the first  
  // MediaPlayer instance. 
  if (!self.mediaAnalyticsProvider1) { 
      self.mediaAnalyticsProvider1 =  
        [[MediaAnalyticsProvider alloc] initWithPlayerDelegate:self.mediaPlayer1]; 
  } 

  // Setup the second media player 
  NSURL *streamUrl2 = [NSURL URLWithString:CONTENT_URL_2]; 

  if (!self.mediaPlayer2) { 
      self.mediaPlayer2 = [[MediaPlayer alloc] initWithContentURL:streamUrl2]; 
      //setup player 
  } 

  // Create the MediaAnalyticsProvider instance and attach it to the second MediaPlayer instance. 
  if (!self.mediaAnalyticsProvider2) { 
      self.mediaAnalyticsProvider2 =  
        [[MediaAnalyticsProvider alloc] initWithPlayerDelegate:self.mediaPlayer2]; 
  } 
} 
```

`MediaAnalyticsProvider` 和 `ADBMediaHeartbeat` 這兩個例項追蹤個別的工作階段，每一個都具有其自己的唯一工作階段 ID。 Charles 除錯工具或除錯記錄中的兩個工作階段，可透過使用工作階段 ID 值來加以識別。

如要在 iOS 上顯示此情境，請設定下列程式碼：

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e., when the 
//    media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 
 
// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

```js
var MediaHeartbeat = ADB.va.MediaHeartbeat; 
var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 

function MediaAnalyticsProvider(player) { 
  if (!player) { 
      throw new Error("Illegal argument. Player reference cannot be null.") 

  } 
  this._player = player; 

  //Media Heartbeat initialization 
  var mediaConfig = new MediaHeartbeatConfig(); 
  mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
  mediaConfig.playerName = Configuration.PLAYER.NAME; 
  mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
  mediaConfig.debugLogging = true; 
  mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
  mediaConfig.ssl = false; 
  mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 

  var mediaDelegate = new MediaHeartbeatDelegate(); 

  mediaDelegate.getCurrentPlaybackTime = function() { 
      return player.getCurrentPlaybackTime(); 
  }; 

  mediaDelegate.prototype.getQoSObject = function() { 
      return player.getQoSInfo(); 
  }; 

  this._mediaHeartbeat =  
    new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
} 
```

```js
// Create first MediaPlayer instance.  
var _player1 = new MediaPlayer(); 

// Create the first MediaAnalyticsProvider instance  
// and attach it to the MediaPlayer instance.  
analyticsProvider1 = new MediaAnalyticsProvider(_player1); 

// Load the main media content.  
_player1.loadContent(URL_TO_MEDIA_1); 

// Create second MediaPlayer instance.  
var _player2 = new MediaPlayer(); 

// Create second MediaAnalyticsProvider instance and 
// attach it to the MediaPlayer instance.  
analyticsProvider2 = new MediaAnalyticsProvider(_player2); 

// Load the main media content for the 2nd player.  
_player2.loadContent(URL_TO_MEDIA_2); 
```

`MediaAnalyticsProvider` 和 `MediaHeartbeat` 這兩個例項追蹤個別的工作階段，每一個都具有其自己的唯一工作階段 ID。 您可以在 Charles 除錯工具中看到兩個工作階段。
