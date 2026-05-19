---
title: 位元速率變更
description: 當播放器切換至不同的位元速率時，引發位元速率變更事件。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# 位元速率變更

>[!BEGINSHADEBOX]

*本頁說明如何實作位元速率變更事件。 檢視對應報表變數的[位元速率變更（維度）](/help/reporting/dimensions/bitrate-changes.md)和[位元速率變更（量度）](/help/reporting/metrics/bitrate-changes.md)。*

>[!ENDSHADEBOX]

位元速率變更事件表示播放器已切換至不同的位元速率。 請先更新QoE物件上的[位元速率](/help/implementation/variables/quality/bitrate.md)值，然後引發位元速率變更事件。 後端會使用這些事件的計數來計算位元速率變更維度和量度，而產生的位元速率值會摘要給平均位元速率。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | （無 — 由後端計算） |
| **XDM事件型別** | `media.bitrateChange` |
| **Audience Manager特徵** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [位元速率變更](/help/implementation/events/playback/bitrate-change.md) |

## Web SDK

使用[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)以新位元速率傳送`media.bitrateChange`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## Mobile SDK

以新的位元速率更新QoE物件，然後引發位元速率變更事件。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

使用`sendMediaEvent`搭配`media.bitrateChange`表示位元速率變更。 在`qoeDataDetails`中包含新的位元速率：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## Media Edge API

使用更新的`qoeDataDetails`呼叫[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## Media SDK

更新QoE物件並引發事件：

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## Media Collection API

傳送具有新位元速率的`bitrateChange` POST要求：

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
