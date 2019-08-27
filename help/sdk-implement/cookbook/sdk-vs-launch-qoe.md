---
seo-title: 瞭解Launch與Media SDK差異
title: 瞭解Launch與Media SDK差異
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# 瞭解Launch與Media SDK差異

## 功能差異

* *Launch* - Launch提供使用者介面，讓您透過設定、設定和部署網頁媒體追蹤解決方案來引導您。啓動改進了動態標籤管理(DTM)。
* *Media SDK* - Media SDK為您提供專為特定平台設計的媒體追蹤程式庫(例如：Android、iOS等)。Adobe建議Media SDK追蹤行動應用程式中的媒體使用情形。

## 追蹤器建立差異

### Launch

Launch提供兩種建立追蹤基礎架構的方法。這兩種方法都使用Media Analytics Launch Extension：

1. 從網頁使用媒體追蹤API。

   在此情況下，Media Analytics Extension會將媒體追蹤API匯出至全域視窗物件中的設定變數：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用其他Launch擴充功能的媒體追蹤API。

   在此情況下，您會使用由 `get-instance` 和 `media-heartbeat` 共用模組公開的媒體追蹤API。

   >[!NOTE]
   >
   >共用模組無法用於網頁中。您只能從其他擴充功能使用共用模組。

   使用 `MediaHeartbeat``get-instance` 共用模組建立例項。
傳遞委派物件至 `get-instance` 展示 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函數。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   透過 `MediaHeartbeat``media-heartbeat` 共用模組存取常數。

### Media SDK

1. 將Media Analytics程式庫新增至您的開發專案。
1. 建立config物件(`MediaHeartbeatConfig`)。
1. 實作委派通訊協定，公開 `getQoSObject()` 和 `getCurrentPlaybackTime()` 功能。
1. 建立媒體心率例項(`MediaHeartbeat`)。

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## 相關文件

### Launch

* [Launch概觀](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [設定JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

