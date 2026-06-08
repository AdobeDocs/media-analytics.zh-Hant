---
title: 廣告插播完成
description: 表示廣告插播中的所有廣告都已完成。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# 廣告插播完成

廣告插播完成事件代表廣告插播中的所有廣告都已完成（已完成或略過）。 它會關閉[廣告插播開始](ad-break-start.md)開啟的廣告插播。

* **必要條件**： [工作階段開始](../session/session-start.md)，[廣告插播開始](ad-break-start.md)
* **關聯的量度**：無

>[!IMPORTANT]
>
>每個`adBreakStart`必須有相符的`adBreakComplete`。 如果沒有結尾書擋，廣告事件會遭忽略，且廣告持續時間會歸因於主要內容。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.adBreakComplete"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

使用`AdBreakComplete`事件型別呼叫`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

使用`AdBreakComplete`事件型別呼叫`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku Edge]

與`eventType: "media.adBreakComplete"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

使用`AdBreakComplete`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

使用`AdBreakComplete`事件型別呼叫`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Roku 2.x]

使用`MEDIA_AD_BREAK_COMPLETE`事件型別呼叫`mediaTrackEvent`：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_COMPLETE)
```

>[!TAB 媒體收集API]

傳送`adBreakComplete`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
