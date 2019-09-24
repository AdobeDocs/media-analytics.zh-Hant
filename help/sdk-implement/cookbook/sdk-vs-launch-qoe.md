---
seo-title: 瞭解Launch與Media SDK的差異
title: 瞭解Launch與Media SDK的差異
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# 瞭解Launch與Media SDK的差異

## 功能差異

* *Launch* - Launch提供您一個UI，可引導您設定、設定和部署網路媒體追蹤解決方案。 Launch在動態標籤管理(DTM)上有所改進。
* *Media SDK* - Media SDK提供您專為特定平台所設計的媒體追蹤程式庫(例如：Android、iOS等)。 Adobe建議使用Media SDK來追蹤行動應用程式中的媒體使用情形。

## 追蹤器建立差異

### Launch

Launch提供兩種建立追蹤基礎架構的方法。 這兩種方法都使用Media Analytics Launch Extension:

1. 使用網頁中的媒體追蹤API。

   在此案例中，媒體分析擴充功能會將媒體追蹤API匯出至全域視窗物件中已設定的變數：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用其他Launch擴充功能的媒體追蹤API。

   在此案例中，您會使用「和共用模組」公開的媒 `get-instance` 體追 `media-heartbeat` 蹤API。

   >[!NOTE]
   >
   >共用模組無法用於網頁。 您只能使用其他擴充功能的共用模組。

   使用共 `MediaHeartbeat` 用模組建立 `get-instance` 例項。
將委派物件傳遞至 `get-instance` 公開 `getQoSObject()` 和函 `getCurrentPlaybackTime()` 數。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   通過 `MediaHeartbeat` 共用模組訪 `media-heartbeat` 問常數。

### Media SDK

1. 將媒體分析程式庫新增至您的開發專案。
1. 建立配置對象(`MediaHeartbeatConfig`)。
1. 實作委派通訊協定，公開 `getQoSObject()` 和函 `getCurrentPlaybackTime()` 數。
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

* [啟動概觀](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA擴充功能](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [設定JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

