---
title: 廣告 ID
description: 唯一識別廣告。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 16%

---


# 廣告 ID

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告ID**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[廣告](/help/reporting/dimensions/ad.md)。*

>[!ENDSHADEBOX]

廣告ID變數可唯一識別每個廣告。 您的播放器追蹤的每個廣告都需使用此功能。 在每個`media.adStart`事件上設定它。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.name` |
| **XDM集合欄位** | [`mediaCollection.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | 廣告開始、廣告關閉 |

## Web SDK

呼叫`media.adStart`的[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingDetails`內設定`name`：

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

## Mobile SDK

將廣告ID作為`adId`引數傳遞給`createAdObject`。 第一個引數(`name`)是好記的名稱；第二個是識別碼。

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

呼叫`media.adStart`的`sendMediaEvent`時，在`mediaCollection.advertisingDetails`中設定`name`：

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

## Media Edge API

呼叫`mediaCollection.advertisingDetails`內有`name`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

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

將廣告ID作為第二個引數傳遞給`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",   // name (friendly name)
  "ad-2125",      // ad ID
  0,              // position in pod
  15              // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

在`adStart` POST要求的`params`物件中包含`media.ad.id`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
