---
title: 廣告完成
description: 代表個別廣告完成播放。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---


# 廣告完成

廣告完成事件代表個別廣告完成播放。 在廣告播放至完成時傳送。 如果檢視器略過廣告，請改為傳送[廣告略過](ad-skip.md)。

* **必要條件**： [工作階段開始](../session/session-start.md)，[廣告插播開始](ad-break-start.md)，[廣告開始](ad-start.md)
* **關聯的量度**： [[!UICONTROL 廣告完成]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>此事件必須由`adBreakStart`和`adBreakComplete`個書檔包圍，即使播放單一廣告亦然。 如果沒有這些書擋，廣告事件會被忽略，而廣告持續時間會計為主要內容持續時間。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.adComplete"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

使用`AdComplete`事件型別呼叫`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

使用`AdComplete`事件型別呼叫`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku]

與`eventType: "media.adComplete"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

使用`AdComplete`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

使用`AdComplete`事件型別呼叫`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB 媒體收集API]

傳送`adComplete`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
