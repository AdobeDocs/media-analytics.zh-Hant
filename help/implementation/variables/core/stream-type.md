---
title: 資料流類型
description: 設定資料流型別，以識別媒體資料流是音訊或視訊內容。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---


# 資料流類型

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**資料流型別**變數的資料集合。 檢視對應報表維度的[資料流型別](/help/reporting/dimensions/stream-type.md)。*

>[!ENDSHADEBOX]

串流型別變數可識別媒體串流是音訊或視訊內容。 所有串流媒體實施都需要此變數，且必須在每個媒體工作階段開始時設定。

正確設定串流型別是串流媒體報表的基礎。 它會啟用Adobe Analytics中的內建&#x200B;**媒體資料流型別**&#x200B;區段（所有媒體、僅限音訊、僅限視訊），並在Customer Journey Analytics中驅動個別的音訊和視訊報表。 它也能確保工作階段資料在媒體分析管道中正確分類。 含有未設定或無效資料流型別的工作階段可能會在下游報表中取消分組或錯誤分類。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.streamType` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`streamType`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

將`Media.MediaType.Video`或`Media.MediaType.Audio`傳遞為`createMediaObject`的`mediaType`引數。 請注意，`createMediaObject`中的`streamType`引數控制內容型別變數（VOD、Live等），而非此變數。

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

呼叫`createMediaSession`時在`mediaCollection.sessionDetails`內設定`streamType`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

呼叫`mediaCollection.sessionDetails`內有`streamType`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "channel": "Sports",
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

將`ADB.Media.MediaType.Video`或`ADB.Media.MediaType.Audio`作為第五個引數傳給`Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`sessionStart` POST要求的`params`物件中包含`media.streamType`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

如需完整的要求結構和所有必要欄位，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
