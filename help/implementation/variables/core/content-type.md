---
title: 內容型別
description: 設定內容型別以識別資料流的格式（VOD、即時、線性、播客、歌曲等）。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---


# 內容型別

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容型別**&#x200B;變數的資料集合。 檢視對應報表維度的[內容型別](/help/reporting/dimensions/content-type.md)。*

>[!ENDSHADEBOX]

內容型別變數會識別資料流的格式(例如，VOD、即時或線性（適用於視訊）或播客或有聲書（適用於音訊）。 所有串流媒體實施都需要它，並且必須在工作階段開始時設定。 Adobe定義的值會填入內建的「內容型別」區段和報表；自訂字串也是可接受的，但不會比對內建區段。 如果未設定，則值預設為`missing_content_type`。

建議值：

* **影片：** `vod`，`live`，`linear`，`ugc`，`dvod`
* **音訊：** `song`，`podcast`，`audiobook`，`radio`

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.contentType` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.contentType` |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`contentType`：

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

傳遞內容型別常數做為`streamType`引數給`createMediaObject`。 使用`MediaConstants.StreamType.*`值，例如`VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`。 注意：在行動SDK中，`streamType`引數會控制內容型別。 資料流型別變數（音訊與視訊）是單獨的`mediaType`引數。

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

呼叫`createMediaSession`時在`mediaCollection.sessionDetails`內設定`contentType`：

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

呼叫`mediaCollection.sessionDetails`內有`contentType`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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

將`ADB.Media.StreamType.*`常數作為第四個引數傳入`ADB.Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`sessionStart` POST要求的`params`物件中包含`media.contentType`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
