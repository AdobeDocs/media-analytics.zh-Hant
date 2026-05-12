---
title: 廣告插播名稱
description: 設定上層廣告插播的易記名稱。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# 廣告插播名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告插播名稱**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[Pod名稱](/help/reporting/dimensions/pod-name.md)。*

>[!ENDSHADEBOX]

廣告插播名稱變數是廣告插播的易記名稱（例如，`"pre-roll"`、`"mid-roll-1"`、`"post-roll"`）。 值是在廣告插播物件上設定，而非個別廣告。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.podFriendlyName` |
| **XDM集合欄位** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **必要** | 是（行動SDK）；否（Edge、媒體收集API） |
| **與**&#x200B;一起傳送 | 廣告開始、廣告關閉 |

## Web SDK

呼叫`media.adBreakStart`的[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingPodDetails`內設定`friendlyName`：

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

## Mobile SDK

將廣告插播名稱作為第一個(`name`)引數傳遞至`createAdBreakObject`，然後在廣告開始事件之前追蹤廣告插播開始事件。

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

呼叫`media.adBreakStart`的`sendMediaEvent`時，在`mediaCollection.advertisingPodDetails`中設定`friendlyName`：

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

## Media Edge API

呼叫`mediaCollection.advertisingPodDetails`內有`friendlyName`的[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

將廣告插播名稱作為第一個引數傳遞給`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Media Collection API

在`adBreakStart` POST要求的`params`物件中包含`media.ad.podFriendlyName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
