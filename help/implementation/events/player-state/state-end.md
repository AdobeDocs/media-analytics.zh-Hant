---
title: 狀態結束
description: 表示媒體播放器已結束追蹤的播放器狀態。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 狀態結束

狀態結束事件表示媒體播放器已退出追蹤狀態，例如全熒幕、靜音或隱藏式字幕。 傳送以關閉[狀態開始](state-start.md)開啟的狀態。 狀態可以在相同的事件呼叫中開始和結束。 播放器可同時結束多個狀態。

有效的狀態名稱： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **必要條件**： [工作階段開始](../session/session-start.md)，[狀態開始](state-start.md)
* **關聯的量度**：因狀態而異；請參閱[追蹤播放器狀態](/help/implementation/events/player-state/overview.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.statesUpdate"`和`statesEnd`中的狀態名稱呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

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

狀態可以在相同呼叫中開始和結束：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

使用狀態物件（從適當的`MediaConstants.PlayerState`常數建立）的`trackPlayerStateEnd`。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

使用狀態物件（從適當的`MediaConstants.PlayerState`常數建立）的`trackPlayerStateEnd`。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Roku]

使用`eventType: "media.statesUpdate"`和`statesEnd`中的狀態名稱呼叫`sendMediaEvent`：

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

呼叫[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)端點，其狀態名稱位於`statesEnd`中：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

搭配適當的`ADBMobile.media.PlayerState`常數使用`ADBMobile.media.createStateObject`：

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB 媒體收集API]

傳送`stateEnd`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
