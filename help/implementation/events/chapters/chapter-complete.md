---
title: 章節完成
description: 表示章節區段已完成播放。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# 章節完成

章節完成事件代表章節已完成播放。 當檢視器到達章節結尾時傳送。 如果檢視器略過章節，請改為傳送[章節略過](chapter-skip.md)。

* **必要條件**： [工作階段開始](../session/session-start.md)，[章節開始](chapter-start.md)
* **關聯的量度**： [章節完成](/help/reporting/metrics/chapter-completes.md)

## Web SDK

與`eventType: "media.chapterComplete"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

使用`ChapterComplete`事件型別呼叫`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku (BrightScript)

與`eventType: "media.chapterComplete"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## Media Edge API

呼叫[chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`ChapterComplete`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## Media Collection API

傳送`chapterComplete`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
