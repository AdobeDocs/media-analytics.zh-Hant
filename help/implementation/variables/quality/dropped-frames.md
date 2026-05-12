---
title: 掉格
description: 設定QoE物件上掉格的執行計數，讓後端可以報告掉格品質。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 12%

---


# 掉格

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**掉格**&#x200B;變數的資料集合。 檢視對應報表維度和量度的[掉格](/help/reporting/dimensions/dropped-frames.md)。*

>[!ENDSHADEBOX]

dropped frames變數是播放器在工作階段期間捨棄的畫面執行計數。 將其設定在QoE物件上，並在播放器回報新資料掉格時更新值。 後端會在工作階段關閉時報告最新值。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.qoe.droppedFrameCount` |
| **XDM集合欄位** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 品質事件，工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.qoeDataDetails`內設定`droppedFrames`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

將捨棄的影格作為第四個引數傳遞給`createQoEObject`。 在任何品質事件引發之前更新追蹤器。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

呼叫`sendMediaEvent`時在`mediaCollection.qoeDataDetails`內設定`droppedFrames`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.qoeDataDetails`內有`droppedFrames`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

將捨棄的影格作為第四個引數傳遞給`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## Media Collection API

在`params`物件中包含`media.qoe.droppedFrames`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
