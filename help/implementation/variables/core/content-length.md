---
title: 內容長度
description: 在工作階段開始時，設定內容長度（以秒為單位）。 這會推動進度標籤和平均每分鐘觀眾數。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# 內容長度

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容長度**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[內容長度](/help/reporting/dimensions/content-length.md)。*

>[!ENDSHADEBOX]

內容長度變數是內容的總持續時間（秒數）。 所有串流媒體實施都需要它，並且必須在工作階段開始時設定。 內容長度可驅動數個後端運算量度，包括進度標籤(10/25/50/75/95%)和平均每分鐘觀眾數。 如果未設定內容長度或不大於零，則不會產生這些量度。 對於持續時間不明的即時資料流，請使用`86400` （24小時）。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.length` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.length` |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`length`：

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

將內容長度（以秒為單位）作為`length`引數傳遞給`createMediaObject`。

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

將內容長度（以秒為單位）作為`length`引數傳遞給`createMediaObject`。

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

呼叫`createMediaSession`時在`xdm.mediaCollection.sessionDetails`內設定`length`：

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

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`length`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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

將內容長度（以秒為單位）作為第三個引數傳給`ADB.Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

將內容長度（以秒為單位）作為第三個引數傳給`ADBMobile.media.createMediaObject`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

將內容長度（以秒為單位）作為第三個引數傳給`adb_media_init_mediainfo`：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.length`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
