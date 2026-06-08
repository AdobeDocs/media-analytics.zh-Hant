---
title: 追蹤播放器狀態
description: 瞭解播放器狀態事件，以及如何追蹤全熒幕、靜音、隱藏式字幕、子母畫面和觀看中狀態。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 12%

---


# 追蹤播放器狀態

播放器狀態事件會追蹤檢視者在整個工作階段中與播放器控制項互動的方式。 核心媒體追蹤實作可選擇使用，且非必要。 五個可追蹤的狀態為： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`和`inFocus`。

播放器狀態事件有助於瞭解協助工具功能的使用情形，例如檢視器啟用隱藏式字幕或靜音的頻率。 此外，還可呈現全熒幕或內嵌檢視、子母畫面多工作業等檢視行為模式。

## 播放器事件

| 播放器事件 | 動作 |
| --- | --- |
| 播放器進入狀態 | 呼叫狀態開始 |
| 播放器結束狀態 | 呼叫狀態結束 |

## 標準和自訂狀態

我們提供 5 種標準播放器狀態，您也可以新增自訂狀態。

| 標準狀態名稱 | Media SDK 常數 | Media Collection API 名稱 |
|----|----|----|
| 全螢幕 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隱藏式字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 靜音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 子母畫面 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 焦點 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

如需包括XDM路徑和量度定義的完整變數參考，請參閱[播放器狀態變數](/help/implementation/variables/player-state/)。

**自訂狀態：**&#x200B;您可以建立自訂狀態來擷取應用程式特有的其他播放器行為。 如需建立自訂狀態物件的詳細資訊，請參閱[媒體API參考： `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)。

## 實作步驟

1. 當播放器進入五個可追蹤的狀態時，**呼叫[狀態開始](state-start.md)**。 可同時啟用多個狀態，且可在相同事件呼叫中啟動多個狀態。
1. 當播放器結束狀態時，**呼叫[狀態結束](state-end.md)**。 可以在相同事件呼叫中結束多個狀態，而且可以在單一呼叫中一起開始和結束狀態。

## 準則

* 一個視訊工作階段 最多能有 10 個播放器狀態。
* 可使用任意的狀態組合。
* 如果傳遞了多個播放器狀態，只有前10個會保留，並轉送給下游的媒體後端。
* 10個狀態的上限適用於所有狀態，無論其為開啟或關閉。
* 狀態可以多次開始和結束，並計為單一狀態。 例如，`closedCaptioning`可以啟動和停止五次，但計為一種狀態。
* 所有播放器狀態都會列入計算 (不分割)
* 系統會分別擷取每個播放工作階段的播放器狀態。 播放器狀態不會跨播放計算。
* 狀態停止後，不會維護應用程式狀態的相關知識。 狀態結束後，狀態必須重新開始才能繼續追蹤。

## 同時更新多個狀態

在XDM平台上，可在`statesStart`和`statesEnd`中使用陣列將多個狀態變更批次處理為單一`statesUpdate`呼叫。 在行動SDK上，每個狀態變更都需要個別呼叫。

下列範例會同時啟動靜音和子母畫面，然後轉換為全熒幕。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

行動SDK不支援批次處理程式 — 針對每個狀態變更傳送個別呼叫。

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

行動SDK不支援批次處理程式 — 針對每個狀態變更傳送個別呼叫。

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku Edge]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

多項狀態變更需要個別呼叫。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

多項狀態變更需要個別呼叫。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB Roku 2.x]

Roku 2.x SDK中不提供播放器狀態追蹤功能。 若要追蹤播放器狀態，請使用[Roku Edge SDK](/help/implementation/edge/roku.md)。

>[!TAB 媒體收集API]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## 長時間暫停

當視訊工作階段的暫停持續時間超過30分鐘時，API需要新的工作階段。 產生新的工作階段ID並保留所有作用中狀態，以便在新的`sessionStart`呼叫後立即透過`stateStart`個事件還原。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

傳送`sessionEnd`之後，開始新的工作階段並立即重新傳送作用中狀態：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## 狀態量度

系統會針對每個追蹤狀態運算三個量度，並在媒體關閉呼叫時傳送至Adobe Analytics：

| 量度 | 內容資料索引鍵 | 說明 |
| --- | --- | --- |
| 狀態集 | `a.media.states.[state.name].set = true` | `true` （若狀態在播放期間設定至少一次） |
| 狀態計數 | `a.media.states.[state.name].count = 4` | 播放期間發生狀態的次數 |
| 狀態時間 | `a.media.states.[state.name].time = 240` | 播放期間花費在狀態的總時間（秒數） |
