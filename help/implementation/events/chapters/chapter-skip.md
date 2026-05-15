---
title: 章節略過
description: 表示檢視器已略過章節。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# 章節略過

章節略過事件表示檢視器在完成章節前已略過章節。 當檢視器導覽超過章節界限時傳送，而不觀看至完成。 如果章節播放到結尾，則傳送[章節完成](chapter-complete.md)。

* **必要條件**： [工作階段開始](../session/session-start.md)，[章節開始](chapter-start.md)
* **關聯的量度**：無

## Web SDK

與`eventType: "media.chapterSkip"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

使用`ChapterSkip`事件型別呼叫`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku (BrightScript)

與`eventType: "media.chapterSkip"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## Media Edge API

呼叫[chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`ChapterSkip`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## Media Collection API

傳送`chapterSkip`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
