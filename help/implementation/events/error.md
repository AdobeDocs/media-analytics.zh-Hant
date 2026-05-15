---
title: 錯誤
description: 表示媒體播放器發生錯誤。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# 錯誤

錯誤事件代表媒體播放器發生錯誤。 追蹤錯誤不會關閉工作階段。 如果錯誤導致無法繼續播放，請在錯誤事件後呼叫[工作階段結束](session/session-end.md)。

* **必要條件**： [工作階段開始](session/session-start.md)
* **關聯的量度**： [錯誤影響的資料流](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source`屬性只接受兩個值： `player` （源自媒體播放器的錯誤）和`external` （來自CDN或網路等外部來源的錯誤）。

## Web SDK

使用`eventType: "media.error"`和必要的`errorDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

使用錯誤識別碼字串呼叫`trackError`。

**iOS (Swift)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android (Kotlin)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku (BrightScript)

使用`eventType: "media.error"`和必要的`errorDetails`來呼叫`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## Media Edge API

使用必要的`errorDetails`呼叫[error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用錯誤識別碼字串呼叫`trackError`：

```javascript
tracker.trackError("media-error-001");
```

## Media Collection API

傳送`error`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
