---
seo-title: 從單機版Media SDK移轉至Adobe Launch - Web(JS)
title: 從單機版Media SDK移轉至Adobe Launch - Web(JS)
seo-description: 說明和程式碼範例，以協助從Media SDK移轉至Launch。
description: 說明和程式碼範例，以協助從Media SDK移轉至Launch。
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# 從單機版Media SDK移轉至Adobe Launch - Web(JS)

## 功能差異

* *Launch* - Launch提供您一個UI，可引導您設定、設定和部署網路媒體追蹤解決方案。 Launch在動態標籤管理(DTM)上有所改進。
* *Media SDK* - Media SDK提供您專為特定平台所設計的媒體追蹤程式庫(例如：Android、iOS等)。 Adobe建議使用Media SDK來追蹤行動應用程式中的媒體使用情形。

## 設定

### 啟動擴充功能

1. 在Experience Platform Launch中，按一下您網頁屬 [!UICONTROL 性的] 「擴充功能」標籤。
1. 在「目 [!UICONTROL 錄] 」標籤上，找到「Adobe Media Analytics for Audio andVideo extension」，然後按一下「 [!UICONTROL 安裝」]。
1. 在擴充功能設定頁面中，設定追蹤參數。
媒體擴充功能會使用已設定的參數進行追蹤。

[啟動使用指南——安裝和配置媒體擴展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

### 獨立媒體SDK

在單機版媒體SDK中，您可在應用程式中設定追蹤設定，並在建立追蹤器時將其傳遞至SDK。

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channe";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

除了設定 `MediaHeartbeat` 外，頁面必須設定並傳遞媒體追蹤的 `AppMeasurement` 例項 `VisitorAPI` 和例項，才能正常運作。

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

[Media SDK —— 建立追蹤器](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

## 相關文件

### Launch

* [啟動概觀](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics擴充功能](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [設定JS](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

