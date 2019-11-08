---
title: 從單機版Media SDK移轉至Adobe Launch - Android
description: 說明和程式碼範例，以協助從Media SDK移轉至Launch for Android。
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# 從單機版Media SDK移轉至Adobe Launch - Android

## 設定

### 獨立媒體SDK

在獨立的Media SDK中，您可在應用程式中設定追蹤，並在建立追蹤器時將其傳遞至SDK。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### 啟動擴充功能

1. 在Experience Platform Launch中，按一下您行動裝置屬 [!UICONTROL 性的] 「擴充功能」標籤。
1. 在「目 [!UICONTROL 錄] 」標籤上，找到Adobe Media Analytics for Audio和Video擴充功能，然後按一下「 [!UICONTROL 安裝」]。
1. 在擴充功能設定頁面中，設定追蹤參數。
媒體擴充功能會使用已設定的參數進行追蹤。

![](assets/launch_config_mobile.png)

[使用Mobile Extensions](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## 建立追蹤器

### 獨立媒體SDK

在獨立的Media SDK中，您可手動建立物 `MediaHeartbeatConfig` 件並設定追蹤參數。 實施委派介面公開`getQoSObject()` , `getCurrentPlaybackTime()functions.`並建立 `MediaHeartbeat` 追蹤的例項。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### 啟動擴充功能

[媒體API參考——建立媒體追蹤器](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

建立追蹤器之前，您應先向行動核心註冊媒體擴充功能和相依擴充功能。

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

註冊媒體擴充功能後，請使用下列API建立追蹤器。
追蹤器會自動從已設定的啟動屬性中挑選設定。

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## 更新播放頭和體驗品質值。

### 獨立媒體SDK

在獨立的Media SDK中，您會傳遞委派物件，在建立追蹤器時`MediaHeartbeartDelegate` ，會建置介面。  當追蹤器呼叫和介面方法時，實作應傳回最新的QoE`getQoSObject()``getCurrentPlaybackTime()` 和播放頭。

### 啟動擴充功能

實作應呼叫追蹤器公開的方法`updateCurrentPlayhead` ，以更新目前播放器播放頭。 為了精確追蹤，您應至少每秒呼叫一次此方法。

[媒體API參考——更新目前的播放器](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

實現應通過調用跟蹤器公開的方法來更 `updateQoEObject`新QoE資訊。 每當品質量度發生變更時，我們預期會呼叫此方法。

[媒體API參考——更新QoE物件](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## 傳遞標準媒體／廣告中繼資料

### 獨立媒體SDK

* 標準媒體中繼資料：

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 標準廣告中繼資料:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```

### 啟動擴充功能

* 標準媒體中繼資料：

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 標準廣告中繼資料:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```
