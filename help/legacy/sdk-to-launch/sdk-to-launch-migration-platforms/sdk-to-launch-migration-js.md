---
title: "從獨立 Media SDK 移轉至 Adobe Launch - Web (JS)"
description: 了解如何從 Media SDK 移轉至 JS 版的 Launch。
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 73ef5e55c9ab57a5a2ba22aa1e4b646c530cc53f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 100%

---

# 從獨立 Media SDK 移轉至 Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch 已經過品牌重塑，現在是 Experience Platform 中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-Hant)。

## 功能差異

* *Launch* - Launch 提供您一個 UI，引導您建立、設定和部署網頁型媒體追蹤解決方案。Launch 可改善 Dynamic Tag Management (DTM)。
* *Media SDK* - Media SDK 提供您專為特定平台 (例如：Android、iOS 等) 所設計的媒體追蹤程式庫。Adobe 建議使用 Media SDK 來追蹤行動應用程式中的媒體使用情形。

## 設定

### 獨立 Media SDK

在獨立 Media SDK 中，您可在應用程式中設定追蹤，
並在建立追蹤器時將其傳遞至 SDK。

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

除了設定 `MediaHeartbeat` 外，頁面必須設定並傳遞
媒體追蹤的 `AppMeasurement` 例項和 `VisitorAPI` 例項
才能正常運作。

### Launch 擴充功能

1. 在 Experience Platform Launch 中，按一下您 Web 屬性的[!UICONTROL 「擴充功能」]
標籤。
1. 在[!UICONTROL 「編目」]標籤上，找到 Adobe Media Analytics for Audio and
Video 擴充功能，然後按一下[!UICONTROL 「安裝」]。
1. 在擴充功能設定頁面中，設定追蹤參數。Media 擴充功能會使用已設定的參數進行追蹤。

   ![](assets/launch_config_js.png)

[Launch 使用手冊 - 安裝和設定媒體擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## 追蹤器建立差異

### Media SDK

1. 將 Media Analytics 程式庫新增至您的開發專案。
1. 建立設定物件 (`MediaHeartbeatConfig`)。
1. 實施委派通訊協定，公開 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函數。
1. 建立 Media Heartbeat 例項 (`MediaHeartbeat`)。

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

### Launch

Launch 提供兩種建立追蹤基礎架構的方法。兩種方法都使用 Media Analytics Launch 擴充功能：

1. 使用網頁中的媒體追蹤 API。

   在此案例中，Media Analytics 擴充功能會將媒體追蹤 API 匯出至全域視窗物件中已設定的變數：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用其他 Launch 擴充功能的媒體追蹤 API。

   在此案例中，您會使用 `get-instance` 和 `media-heartbeat`「共用模組」公開的媒體追蹤 API。

   >[!NOTE]
   >
   >「共用模組」不適用於網頁。您只能使用其他擴充功能的「共用模組」。

   使用 `get-instance`「共用模組」建立 `MediaHeartbeat` 例項。
將委派物件傳遞至 `get-instance` 公開的 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函數。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   透過 `media-heartbeat`「共用模組」存取 `MediaHeartbeat` 常數。

## 相關文件

### Media SDK

* [設定 JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch 概述](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hant)
* [Media Analytics 擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
