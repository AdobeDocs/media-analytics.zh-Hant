---
title: 章節位移
description: 設定內容內章節的位移（以秒為單位），從頭開始。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 12%

---


# 章節位移

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**章節位移**變數的資料集合。 如需對應的報表維度，請參閱[章節位移](/help/reporting/dimensions/chapter-offset.md)。*

>[!ENDSHADEBOX]

章節位移變數是內容中章節的位移，以秒為單位，從頭開始測量。 第一個章節通常具有位移`0`；後續章節具有與其播放點開始時間相符的位移。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.chapter.offset` |
| **XDM集合欄位** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **必要** | 否（行動SDK）；是（Edge、媒體收集API） |
| **與**&#x200B;一起傳送 | 章節開始、章節關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.chapterDetails`內設定`offset`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

以秒為單位傳遞位移作為第四個引數(`startTime`)至`createChapterObject`。

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

呼叫`media.chapterStart`的`sendMediaEvent`時，在`mediaCollection.chapterDetails`中設定`offset`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.chapterDetails`內有`offset`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## Media SDK

將位移作為第四個引數傳遞給`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Media Collection API

在`chapterStart` POST要求的`params`物件中包含`media.chapter.offset`：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
