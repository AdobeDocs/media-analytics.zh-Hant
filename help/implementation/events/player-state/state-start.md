---
title: 狀態開始
description: 表示媒體播放器進入追蹤的播放器狀態。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 6%

---


# 狀態開始

狀態開始事件表示媒體播放器進入追蹤狀態，例如全熒幕、靜音或隱藏式字幕。 播放器可同時處於多個狀態，且狀態可在相同事件呼叫中開始和結束。 以[狀態end](state-end.md)事件關閉每個狀態。

有效的狀態名稱： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**：因狀態而異；請參閱[追蹤播放器狀態](/help/implementation/events/player-state/overview.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.statesUpdate"`和`statesStart`中的狀態名稱呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

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

可以在相同呼叫中開始多個狀態：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

使用狀態物件（從適當的`MediaConstants.PlayerState`常數建立）的`trackPlayerStateStart`。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

使用狀態物件（從適當的`MediaConstants.PlayerState`常數建立）的`trackPlayerStateStart`。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.statesUpdate"`和`statesStart`中的狀態名稱呼叫`sendMediaEvent`：

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

>[!TAB Media Edge API]

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其狀態名稱位於`statesStart`中：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

搭配適當的`ADB.Media.PlayerState`常數使用`ADB.Media.createStateObject`：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

搭配適當的`ADBMobile.media.PlayerState`常數使用`ADBMobile.media.createStateObject`：

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB Roku 2.x]

Roku 2.x SDK中不提供播放器狀態追蹤功能。 若要追蹤播放器狀態，請使用[Roku Edge SDK](/help/implementation/edge/roku.md)。

>[!TAB 媒體收集API]

傳送`stateStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
