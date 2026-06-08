---
title: 廣告插播開始
description: 代表廣告插播開始（一或多個廣告的序列）。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# 廣告插播開始

廣告插播開始事件代表廣告插播開始。 廣告插播是一或多個廣告的序列。 每個`adStart`、`adComplete`和`adSkip`事件都必須在`adBreakStart`和`adBreakComplete`對之間發生，即使播放單一廣告亦然。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**：無

>[!IMPORTANT]
>
>已忽略廣告事件(`adStart`、`adComplete`、`adSkip`)，但不包含`adBreakStart`和`adBreakComplete`個書擋。 如果沒有這些變數，廣告持續時間會歸因於主要內容持續時間，而這會影響彙總的報表資料。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.adBreakStart"`和必要的`advertisingPodDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將廣告插播名稱、位置和開始時間傳遞至`createAdBreakObject`，然後呼叫`trackEvent`。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

將廣告插播名稱、位置和開始時間傳遞至`createAdBreakObject`，然後呼叫`trackEvent`。

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.adBreakStart"`和必要的`advertisingPodDetails`來呼叫`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

使用必要的`advertisingPodDetails`呼叫[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
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

將廣告插播名稱、位置和開始時間傳遞至`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

將廣告插播名稱、位置和開始時間傳遞至`ADBMobile.media.createAdBreakObject`：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

使用`adb_media_init_adbreakinfo`建立廣告插播物件，然後追蹤事件。 請注意Roku引數順序： `name, startTime, position`。

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB 媒體收集API]

傳送`adBreakStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```

>[!ENDTABS]
