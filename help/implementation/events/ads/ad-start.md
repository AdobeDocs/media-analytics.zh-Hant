---
title: 廣告開始
description: 表示個別廣告開始播放。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 7%

---


# 廣告開始

廣告開始事件代表個別廣告開始播放。 它必須出現在[廣告插播開始](ad-break-start.md) / [廣告插播完成](ad-break-complete.md)配對中。

* **必要條件**： [工作階段開始](../session/session-start.md)，[廣告插播開始](ad-break-start.md)
* **關聯的量度**： [[!UICONTROL 廣告開始]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>此事件必須由`adBreakStart`和`adBreakComplete`個書檔包圍，即使播放單一廣告亦然。 如果沒有這些書擋，廣告事件會被忽略，而廣告持續時間會計為主要內容持續時間。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.adStart"`和必要的`advertisingDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將廣告名稱、ID、Pod位置和長度傳遞至`createAdObject`，然後呼叫`trackEvent`。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

將廣告名稱、ID、Pod位置和長度傳遞至`createAdObject`，然後呼叫`trackEvent`。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.adStart"`和必要的`advertisingDetails`來呼叫`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

使用必要的`advertisingDetails`呼叫[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

將廣告名稱、ID、位置和長度傳遞至`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB Chromecast]

將廣告名稱、ID、位置和長度傳遞至`ADBMobile.media.createAdObject`：

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

使用`adb_media_init_adinfo`建立廣告物件，然後追蹤事件。 Pod內的廣告位置是以1為基底。

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 15.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒體收集API]

傳送`adStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
