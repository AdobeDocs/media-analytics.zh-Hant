---
title: 廣告略過
description: 表示檢視器略過廣告。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# 廣告略過

廣告略過事件表示檢視器在完成之前已略過廣告。 當檢視者選取略過按鈕時傳送。 如果廣告播放到完成，請改為傳送[廣告完成](ad-complete.md)。

* **必要條件**： [工作階段開始](../session/session-start.md)，[廣告插播開始](ad-break-start.md)，[廣告開始](ad-start.md)
* **關聯的量度**：無

>[!IMPORTANT]
>
>此事件必須由`adBreakStart`和`adBreakComplete`個書檔包圍，即使播放單一廣告亦然。 如果沒有這些書擋，廣告事件會被忽略，而廣告持續時間會計為主要內容持續時間。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

使用`AdSkip`事件型別呼叫`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

使用`AdSkip`事件型別呼叫`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Roku]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`AdSkip`事件型別呼叫`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB Chromecast]

使用`AdSkip`事件型別呼叫`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB 媒體收集API]

傳送`adSkip`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
