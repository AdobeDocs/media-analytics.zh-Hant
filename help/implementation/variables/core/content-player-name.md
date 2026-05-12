---
title: 內容播放器名稱
description: 設定播放器名稱以識別轉譯了內容的播放器。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# 內容播放器名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容播放器名稱**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[內容播放器名稱](/help/reporting/dimensions/content-player-name.md)。*

>[!ENDSHADEBOX]

內容播放器名稱變數會識別轉譯內容的播放器（例如，`HTML5 Player`、`Brightcove`或`Roku Player`）。 所有串流媒體實施都需要它，並且必須在工作階段開始時設定。 此值用於「內容播放器名稱」維度，以比較相同屬性中不同播放器的參與度和品質。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.playerName` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`playerName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

使用`MediaConstants.TrackerConfig.PLAYER_NAME`建立追蹤器時，透過追蹤器設定設定播放器名稱。 播放器名稱不是媒體物件的一部分。

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

呼叫`createMediaSession`時在`mediaCollection.sessionDetails`內設定`playerName`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`playerName`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

在建立追蹤器之前，先在`ADB.MediaConfig`上設定播放器名稱：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## Media Collection API

在`sessionStart` POST要求的`params`物件中包含`media.playerName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
