---
title: 焦點
description: 追蹤播放器何時聚焦在檢視者的畫面，讓後端可以報告焦點參與情形。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 9%

---


# 焦點

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**焦點**&#x200B;播放器狀態的資料集合。 檢視對應報表量度的受焦點影響的[資料流](/help/reporting/metrics/in-focus-streams-impacted.md)、[焦點計數](/help/reporting/metrics/in-focus-count.md)以及[焦點總持續時間](/help/reporting/metrics/in-focus-total-duration.md)。*

>[!ENDSHADEBOX]

觀看中播放器狀態會追蹤播放器何時吸引檢視者的注意。 在播放器獲得焦點時（通常是播放器索引標籤或視窗成為作用中時），引發狀態開始事件，並在播放器失去焦點時引發狀態結束事件。 後端會從這些事件計算三個量度：受影響的資料流、狀態專案計數和狀態總時間。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **XDM集合欄位** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)和[`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （含有`name: "inFocus"`的專案） |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 狀態開始、狀態結束 |

## Web SDK

使用[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

當播放器失焦時，傳送另一個狀態為`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.IN_FOCUS`常數搭配使用。

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

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
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

當播放器失焦時，傳送另一個狀態為`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其中`statesStart`有`inFocus` （或播放器失焦時的`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.InFocus`常數：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Media Collection API

在播放器獲得焦點時傳送`stateStart` POST要求，並在失焦時傳送`stateEnd` POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
