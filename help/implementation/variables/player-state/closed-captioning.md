---
title: 隱藏式字幕
description: 追蹤檢視器何時開啟和關閉隱藏式字幕，以便後端可以報告字幕參與情形。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 5%

---


# 隱藏式字幕

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**隱藏式字幕**播放器狀態的資料集合。 如需對應的報表量度，請參閱[受隱藏式字幕影響的資料流](/help/reporting/metrics/closed-captioning-streams-impacted.md)、[隱藏式字幕計數](/help/reporting/metrics/closed-captioning-count.md)和[隱藏式字幕總時間](/help/reporting/metrics/closed-captioning-total-duration.md)。*

>[!ENDSHADEBOX]

隱藏式字幕播放器狀態會追蹤檢視器何時開啟及關閉字幕。 在啟用註解時引發狀態開始事件，並在停用註解時引發狀態結束事件。 後端會從這些事件計算三個量度：受影響的資料流、狀態專案計數和狀態總時間。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **XDM集合欄位** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （含有`name: "closedCaptioning"`的專案） |
| **Audience Manager特徵** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
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
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

當檢視器停用註解時，傳送另一個狀態為`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.CLOSED_CAPTION`常數搭配使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

將`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`與`MediaConstants.PlayerState.CLOSED_CAPTION`常數搭配使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

使用`sendMediaEvent`傳送狀態已新增至`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

當檢視器停用註解時，傳送另一個狀態為`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其中`statesStart`中有`closedCaptioning` （或在檢視器停用註解時`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
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

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.ClosedCaptioning`常數：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接將`ADBMobile.media.createStateObject`與`"closedCaptioning"`字串搭配使用，因為Chromecast尚未命名`PlayerState`常數：

```javascript
var stateObject = ADBMobile.media.createStateObject("closedCaptioning");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer disables captions:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Roku 2.x SDK中不提供播放器狀態追蹤功能。 若要追蹤播放器狀態，請使用[Roku Edge SDK](/help/implementation/edge/roku.md)。

>[!TAB 媒體收集API]

啟用註解時傳送`stateStart` POST要求，停用註解時傳送`stateEnd` POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
