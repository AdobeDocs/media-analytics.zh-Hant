---
title: 工作階段完成
description: 表示檢視器已到達主要內容的結尾。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# 工作階段完成

工作階段完成事件代表檢視器已到達主要內容的結尾。 它不會立即關閉工作階段；工作階段會保持開啟狀態，直到它自然過期為止。 如果要立即關閉工作階段，請改為呼叫[工作階段結束](session-end.md)。

* **必要條件**： [工作階段開始](session-start.md)
* **關聯的量度**： [內容完成](/help/reporting/metrics/content-completes.md)

## Web SDK

與`eventType: "media.sessionComplete"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## Mobile SDK

當媒體播放器到達內容結尾時，呼叫`trackComplete`。

**iOS (Swift)**

```swift
tracker.trackComplete()
```

**Android (Kotlin)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

與`eventType: "media.sessionComplete"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## Media Edge API

呼叫[sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

當媒體播放器到達內容結尾時，呼叫`trackComplete`：

```javascript
tracker.trackComplete();
```

## Media Collection API

傳送`sessionComplete`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
