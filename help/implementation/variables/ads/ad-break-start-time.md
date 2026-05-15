---
title: 廣告插播開始時間
description: 設定內容內廣告插播的開始時間（位移） （以秒為單位）。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---


# 廣告插播開始時間

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告插播開始時間**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[Pod位置](/help/reporting/dimensions/pod-position.md)。*

>[!ENDSHADEBOX]

廣告插播開始時間變數是內容內廣告插播的位移（以秒為單位）。 對於前段播放，值為`0`；對於中段播放，值是插播開始的播放點位置。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.podSecond` |
| **XDM集合欄位** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.podSecond` |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | [廣告插播開始](/help/implementation/events/ads/ad-break-start.md)，廣告關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingPodDetails`內設定`offset`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

將開始時間（以秒為單位）作為第三個引數傳給`createAdBreakObject`。

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

呼叫`media.adBreakStart`的`sendMediaEvent`時，在`mediaCollection.advertisingPodDetails`中設定`offset`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.advertisingPodDetails`內有`offset`的[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

將開始時間作為第三個引數傳給`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Media Collection API

在`adBreakStart` POST要求的`params`物件中包含`media.ad.podSecond`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
