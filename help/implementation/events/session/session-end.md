---
title: 工作階段結束
description: 當檢視器放棄內容時，立即關閉媒體工作階段。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# 工作階段結束

工作階段結束事件會立即關閉媒體追蹤工作階段。 當檢視器在到達結尾之前放棄內容，而您不想在同一工作階段下追蹤後續事件時，請使用它。 如果檢視器完成內容，請改為呼叫[工作階段完成](session-complete.md)。

如果沒有明確的工作階段結束，工作階段會在沒有事件的10分鐘或播放點沒有移動的30分鐘後自動關閉。

* **必要條件**： [工作階段開始](session-start.md)
* **關聯的量度**：無

## Web SDK

與`eventType: "media.sessionEnd"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

當檢視器關閉播放器或導覽離開時，請呼叫`trackSessionEnd`。

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

與`eventType: "media.sessionEnd"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

呼叫[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

當檢視器關閉播放器或導覽離開時呼叫`trackSessionEnd`：

```javascript
tracker.trackSessionEnd();
```

## Media Collection API

傳送`sessionEnd`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
