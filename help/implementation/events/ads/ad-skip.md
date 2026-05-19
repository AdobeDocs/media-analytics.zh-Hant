---
title: 廣告略過
description: 表示檢視器略過廣告。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# 廣告略過

廣告略過事件表示檢視器在完成之前已略過廣告。 當檢視者選取略過按鈕時傳送。 如果廣告播放到完成，請改為傳送[廣告完成](ad-complete.md)。

* **必要條件**： [工作階段開始](../session/session-start.md)，[廣告插播開始](ad-break-start.md)，[廣告開始](ad-start.md)
* **關聯的量度**：無

>[!IMPORTANT]
>
>此事件必須由`adBreakStart`和`adBreakComplete`個書檔包圍，即使播放單一廣告亦然。 如果沒有這些書擋，廣告事件會被忽略，而廣告持續時間會計為主要內容持續時間。

## Web SDK

與`eventType: "media.adSkip"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## Mobile SDK

使用`AdSkip`事件型別呼叫`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku (BrightScript)

與`eventType: "media.adSkip"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## Media Edge API

呼叫[adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`AdSkip`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## Media Collection API

傳送`adSkip`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
