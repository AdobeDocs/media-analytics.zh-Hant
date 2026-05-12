---
title: Pod位置中的廣告
description: 將廣告的索引位置設定在其上層廣告插播中。 第一個廣告索引為0。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---


# Pod位置中的廣告

>[!BEGINSHADEBOX]

*本頁涵蓋pod position **變數中**&#x200B;廣告的資料集合。 如需對應的報表維度，請參閱Pod位置[&#128279;](/help/reporting/dimensions/ad-in-pod-position.md)中的廣告。*

>[!ENDSHADEBOX]

Pod位置變數中的廣告是廣告在其上層廣告插播中的零索引位置。 Pod中的第一個廣告索引為`0`，第二個廣告索引為`1`，依此類推。 使用維度可依廣告插播中的位置比較參與和完成情形。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.podPosition` |
| **XDM集合欄位** | [`mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | 廣告開始、廣告關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingDetails`內設定`podPosition`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

將位置作為第三個引數傳給`createAdObject`。

**iOS (Swift)**

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

## Roku (BrightScript)

呼叫`media.adStart`的`sendMediaEvent`時，在`mediaCollection.advertisingDetails`中設定`podPosition`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.advertisingDetails`內有`podPosition`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

將位置作為第三個引數傳給`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.ad.podPosition`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
