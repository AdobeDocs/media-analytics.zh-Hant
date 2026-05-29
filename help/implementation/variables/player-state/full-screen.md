---
title: 全螢幕
description: 追蹤檢視器何時進入和結束全熒幕播放，讓後端可以報告全熒幕參與度。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---


# 全螢幕

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**全熒幕**播放器狀態的資料集合。 檢視對應報表量度受全熒幕影響的[資料流](/help/reporting/metrics/full-screen-streams-impacted.md)、[全熒幕計數](/help/reporting/metrics/full-screen-count.md)及[全熒幕總持續時間](/help/reporting/metrics/full-screen-total-duration.md)。*

>[!ENDSHADEBOX]

全熒幕播放器狀態會追蹤檢視器何時進入和退出全熒幕播放。 每當檢視器進入全熒幕時引發狀態開始事件，並在檢視器退出時引發狀態結束事件。 後端會從這些事件計算三個量度：受影響的資料流、狀態專案計數和狀態總時間。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **XDM集合欄位** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （含有`name: "fullscreen"`的專案） |
| **Audience Manager特徵** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [狀態開始](/help/implementation/events/player-state/state-start.md)，[狀態結束](/help/implementation/events/player-state/state-end.md) |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

當檢視器退出全熒幕時，傳送另一個狀態為`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.FULLSCREEN`常數搭配使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.FULLSCREEN`常數搭配使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

使用`sendMediaEvent`傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

當檢視器退出全熒幕時，傳送另一個狀態為`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其中`statesStart`中有`fullscreen` （或在檢視器退出時有`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.FullScreen`常數：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接將`ADBMobile.media.createStateObject`與`"fullscreen"`字串搭配使用，因為Chromecast尚未命名`PlayerState`常數：

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB 媒體收集API]

當檢視者進入全熒幕時傳送`stateStart`個POST要求，而當檢視者退出時傳送`stateEnd`個POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
