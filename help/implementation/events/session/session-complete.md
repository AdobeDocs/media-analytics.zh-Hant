---
title: 工作階段完成
description: 表示檢視器已到達主要內容的結尾。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# 工作階段完成

工作階段完成事件代表檢視器已到達主要內容的結尾。 它不會立即關閉工作階段；工作階段會保持開啟狀態，直到它自然過期為止。 如果要立即關閉工作階段，請改為呼叫[工作階段結束](session-end.md)。

* **必要條件**： [工作階段開始](session-start.md)
* **關聯的量度**： [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

當媒體播放器到達內容結尾時，呼叫`trackComplete`。

```swift
tracker.trackComplete()
```

>[!TAB Android]

當媒體播放器到達內容結尾時，呼叫`trackComplete`。

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

當媒體播放器到達內容結尾時，呼叫`trackComplete`：

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

當媒體播放器到達內容結尾時，呼叫`trackComplete`：

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

當媒體播放器到達內容結尾時，呼叫`mediaTrackComplete`：

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB 媒體收集API]

傳送`sessionComplete`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
