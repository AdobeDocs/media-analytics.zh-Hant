---
title: 子母畫面
description: 追蹤檢視器何時進入和結束子母畫面播放，讓後端可以報告PiP參與情形。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 8%

---


# 子母畫面

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**子母畫面**&#x200B;播放器狀態的資料集合。 檢視對應報表量度的[受子母畫面影響的資料流](/help/reporting/metrics/picture-in-picture-streams-impacted.md)、[子母畫面計數](/help/reporting/metrics/picture-in-picture-count.md)和[子母畫面總持續時間](/help/reporting/metrics/picture-in-picture-total-duration.md)。*

>[!ENDSHADEBOX]

子母畫面播放器狀態會追蹤檢視者進入和退出子母畫面播放的時間。 當子母畫面開始時引發狀態開始事件，而當子母畫面結束時引發狀態結束事件。 後端會從這些事件計算三個量度：受影響的資料流、狀態專案計數和狀態總時間。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **XDM集合欄位** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-collection-details)和[`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-collection-details) （含有`name: "pictureInPicture"`的專案） |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 狀態開始、狀態結束 |

## Web SDK

使用[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

當檢視器結束子母畫面時，傳送另一個狀態為`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.PICTURE_IN_PICTURE`常數搭配使用。

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

使用`sendMediaEvent`傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

當檢視器結束子母畫面時，傳送另一個狀態為`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其中`statesStart`有`pictureInPicture` （或檢視器結束PiP時有`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.PictureInPicture`常數：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Media Collection API

當子母畫面開始時會傳送`stateStart` POST要求，並在畫面結束時傳送`stateEnd` POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
