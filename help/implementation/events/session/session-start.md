---
title: 工作階段開始
description: 代表媒體工作階段開始，並取得所有後續事件所需的工作階段ID。
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# 工作階段開始

工作階段開始事件會開啟媒體追蹤工作階段。 此事件必須是任何播放所傳送的第一個事件。 回應會傳回相同工作階段的所有後續事件都必須包含的工作階段ID。

如果&#x200B;**在10分鐘內未收到任何事件**，或是&#x200B;**在30分鐘內沒有播放點移動**，工作階段會自動過期。 如果工作階段過期，您必須再次呼叫工作階段開始以取得新的工作階段ID。

* **必要條件**：無；永遠是第一個事件
* **關聯的量度**： [媒體開始](/help/reporting/metrics/media-starts.md)

## Web SDK

使用`eventType: "media.sessionStart"`和必要的`sessionDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)。 回應包含`handle[].payload[].sessionId`中的工作階段識別碼（型別`media-analytics:new-session`）。 儲存這個值，並在所有後續事件中以`sessionID`的形式傳遞。

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

使用媒體物件和選擇性中繼資料呼叫`trackSessionStart`。

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

使用必要的階段作業詳細資料呼叫`createMediaSession`：

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

呼叫[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點。 回應包含`handle[].payload[].sessionId`中的工作階段識別碼（型別`media-analytics:new-session`）。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## Media SDK

使用使用`ADB.Media.createMediaObject`建立的媒體物件來呼叫`trackSessionStart`：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## Media Collection API

傳送`sessionStart`張貼至[工作階段端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。 回應`Location`標頭包含要用於所有後續事件要求的工作階段識別碼。

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
