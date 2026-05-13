---
title: 從獨立Media SDK移轉至Adobe Launch - Web (JS)
description: 了解如何從 Media SDK 移轉至 JS 版的 Launch。
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c069c44e-5426-4c1a-accc-8028662f2fdeid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# 從獨立 Media SDK 移轉至 Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch 已經過品牌重塑，現在是 Experience Platform 中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-TW)。

## 功能差異

* *Launch* - Launch 提供您一個 UI，引導您建立、設定和部署網頁型媒體追蹤解決方案。 Launch 可改善 Dynamic Tag Management (DTM)。
* *Media SDK* - Media SDK 提供您專為特定平台 (例如：Android、iOS 等) 所設計的媒體追蹤程式庫。 Adobe 建議使用 Media SDK 來追蹤行動應用程式中的媒體使用情形。

## 設定

### 獨立 Media SDK

在獨立Media SDK中，您可在應用程式中設定追蹤設定
並在建立追蹤器時將其傳遞至SDK。

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

除了`MediaHeartbeat`設定外，頁面還必須設定並傳遞
媒體追蹤的`AppMeasurement`執行個體和`VisitorAPI`執行個體依序排列
以正常運作。

### Launch 擴充功能

1. 在Experience Platform Launch中，按一下您專屬的[!UICONTROL 擴充功能]標籤
Web屬性。
1. 在[!UICONTROL 目錄]標籤上，找到Adobe Media Analytics for Audio並
視訊延伸模組，然後按一下[安裝]。
1. 在擴充功能設定頁面中，設定追蹤參數。
Media 擴充功能會使用已設定的參數進行追蹤。

   ![](assets/launch_config_js.png)

[Launch使用手冊 — 安裝和設定媒體擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

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

Launch 提供兩種建立追蹤基礎架構的方法。 兩種方法都使用 Media Analytics Launch 擴充功能：

1. 使用網頁中的媒體追蹤 API。

   在此案例中，Media Analytics 擴充功能會將媒體追蹤 API 匯出至全域視窗物件中已設定的變數：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用其他 Launch 擴充功能的媒體追蹤 API。

   在此案例中，您會使用 `get-instance` 和 `media-heartbeat`「共用模組」公開的媒體追蹤 API。

   >[!NOTE]
   >
   >「共用模組」不適用於網頁。 您只能使用其他擴充功能的「共用模組」。

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

* [Launch概觀](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Media Analytics擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
