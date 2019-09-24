---
seo-title: 繼續非作用中工作階段
title: 繼續非作用中工作階段
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 繼續非作用中工作階段{#resuming-inactive-sessions}

## 長暫停

Media SDK會自動追蹤媒體播放在下列非作用中狀態中的時間長度：

* 已暫停
* 搜尋
* 已停止
* 緩衝處理

如果媒體追蹤工作階段在非活動狀態中停留超過30分鐘，工作階段會自動關閉。 如果使用者在先前的非作用中視訊追蹤工作階段之後繼續 (`trackPlay`)，媒體心率會使用先前使用的視訊資訊和中繼資料自動建立新視訊工作階段，並傳送繼續心率事件。For more information, see [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

## 手動繼續先前關閉的工作階段

Media SDK只有在應用程式未關閉時才會自動繼續工作階段。 如果應用程式儲存用戶資料並能夠恢復先前關閉的介質，則可以手動觸發恢復事件。 開始視訊追蹤工作階段時，請設定選用的 Video Resumed 屬性。

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS 

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

