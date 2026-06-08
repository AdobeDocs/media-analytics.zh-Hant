---
title: 內容管道
description: 設定頻道以識別播放內容的分發站台、網路或屬性。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 6%

---


# 內容管道

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容管道**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[內容管道](/help/reporting/dimensions/content-channel.md)。*

>[!ENDSHADEBOX]

內容頻道變數可識別播放內容的分發站台、網路或屬性。 所有串流媒體實施都需要它。 可接受任何字串。 典型值包括網路名稱、網站路徑的一部分或內部屬性識別碼。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.channel` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.channel` |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`channel`：

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

>[!TAB iOS]

使用`MediaConstants.TrackerConfig.CHANNEL`建立追蹤器時，透過追蹤器設定設定頻道。 頻道不是媒體物件的一部分。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

使用`MediaConstants.TrackerConfig.CHANNEL`建立追蹤器時，透過追蹤器設定設定頻道。 頻道不是媒體物件的一部分。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

呼叫`createMediaSession`時在`xdm.mediaCollection.sessionDetails`內設定`channel`：

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

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`channel`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

在建立追蹤器之前，請先在`ADB.MediaConfig`上設定頻道：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

呼叫`trackSessionStart`時傳遞`channel`作為標準中繼資料索引鍵：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.channel": "Sports" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

在`ADBMobileConfig.json`的`mediaHeartbeat`區段中設定`channel`。 通道是設定值，而非每個工作階段值：

```json
"mediaHeartbeat": {
  "channel": "Sports"
}
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.channel`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
