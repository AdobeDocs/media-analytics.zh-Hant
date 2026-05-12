---
title: 位元速率
description: 在QoE物件上設定目前的播放位元速率（以每秒位元組數為單位），讓後端可以計算位元速率量度。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# 位元速率

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**位元速率**&#x200B;變數的資料集合。 檢視對應報表變數的[平均位元速率（維度）](/help/reporting/dimensions/average-bitrate.md)和[平均位元速率（量度）](/help/reporting/metrics/average-bitrate.md)。*

>[!ENDSHADEBOX]

位元速率變數是目前播放位元速率（以每秒千位元為單位）。 每當播放器交涉位元速率時，請在QoE物件上設定它，並在位元速率變更時更新QoE物件。 後端會使用位元速率值來計算平均位元速率、每個位元速率貯體維度，以及位元速率變更量度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.qoe.bitrateAverageBucket` |
| **XDM集合欄位** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 品質事件（位元速率變更、緩衝、錯誤）、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`media.bitrateChange` （或任何品質相關事件）的`mediaCollection.qoeDataDetails`中設定`bitrate`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

將位元速率作為第一個引數傳給`createQoEObject`。 在任何品質事件引發之前更新追蹤器上的QoE物件。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

呼叫`media.bitrateChange`等品質事件的`sendMediaEvent`時，在`mediaCollection.qoeDataDetails`內設定`bitrate`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.qoeDataDetails`內有`bitrate`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

將位元速率作為第一個引數傳遞給`ADB.Media.createQoEObject`並更新追蹤器：

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## Media Collection API

在`bitrateChange` POST要求的`params`物件中包含`media.qoe.bitrate`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
