---
title: 位元速率變更
description: 表示播放位元速率已變更。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 14%

---


# 位元速率變更

位元速率變更事件表示播放器交涉了新的播放位元速率。 每當播放期間位元速率變更時傳送。 在QoE資料中包含新的位元速率值，讓後端可以計算[平均位元速率](/help/reporting/metrics/average-bitrate.md)和每個位元速率貯體維度。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**： [位元速率變更](/help/reporting/metrics/bitrate-changes.md)

## Web SDK

以`eventType: "media.bitrateChange"`呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)，新位元速率為`qoeDataDetails`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

使用新位元速率建立QoE物件，並在引發位元速率變更事件之前更新追蹤器。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

以`eventType: "media.bitrateChange"`呼叫`sendMediaEvent`，新位元速率為`qoeDataDetails`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

在`qoeDataDetails`中使用新位元速率呼叫[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用新位元速率建立QoE物件並更新追蹤器：

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## Media Collection API

傳送`bitrateChange` POST至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)，新位元速率為`qoeData`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```
