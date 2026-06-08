---
title: 緩衝開始
description: 表示媒體播放器進入緩衝狀態。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%

---


# 緩衝開始

緩衝開始事件代表媒體播放器進入緩衝狀態。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**： [[!UICONTROL 緩衝事件]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**以XDM為基礎的API (Web SDK、Roku、Media Edge API、Media Collection API)：**&#x200B;沒有緩衝恢復事件型別；當您在`bufferStart`之後傳送[`play`](play.md)事件時推斷為緩衝結束。
>
>**行動SDK：**&#x200B;在播放器結束緩衝時呼叫`trackEvent(BufferComplete)`，然後呼叫`trackPlay()`以繼續播放。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.bufferStart"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

當播放器進入緩衝狀態時，使用`BufferStart`呼叫`trackEvent`，當播放器結束時呼叫`BufferComplete`。

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

當播放器進入緩衝狀態時，使用`BufferStart`呼叫`trackEvent`，當播放器結束時呼叫`BufferComplete`。

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku Edge]

與`eventType: "media.bufferStart"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
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

使用`BufferStart`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

當播放器進入緩衝狀態時，使用`BufferStart`呼叫`trackEvent`，當播放器結束時呼叫`BufferComplete`：

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

當播放器進入緩衝狀態時，使用`MEDIA_BUFFER_START`呼叫`mediaTrackEvent`，當播放器結束時呼叫`MEDIA_BUFFER_COMPLETE`：

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB 媒體收集API]

傳送`bufferStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
