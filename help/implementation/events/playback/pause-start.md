---
title: 暫停開始
description: 表示使用者已暫停媒體播放。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# 暫停開始

暫停開始事件表示使用者已暫停播放。 沒有單獨的繼續事件；繼續播放時傳送[播放](play.md)事件。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **相關聯的量度**： [[!UICONTROL 暫停事件]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>沒有繼續事件型別。 當您在`pauseStart`之後傳送[`play`](play.md)事件時會推斷為繼續。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.pauseStart"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

當使用者暫停播放時，呼叫`trackPause`。

```swift
tracker.trackPause()
```

>[!TAB Android]

當使用者暫停播放時，呼叫`trackPause`。

```kotlin
tracker.trackPause()
```

>[!TAB Roku Edge]

與`eventType: "media.pauseStart"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

當使用者暫停播放時，呼叫`trackPause`：

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

當使用者暫停播放時，呼叫`trackPause`：

```javascript
ADBMobile.media.trackPause();
```

>[!TAB Roku 2.x]

當使用者暫停播放時，呼叫`mediaTrackPause`：

```brightscript
ADBMobile().mediaTrackPause()
```

>[!TAB 媒體收集API]

傳送`pauseStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
