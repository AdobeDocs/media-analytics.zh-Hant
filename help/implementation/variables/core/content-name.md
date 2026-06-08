---
title: 內容名稱
description: 設定內容的易記名稱（報表中顯示的可讀取標題）。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 8%

---


# 內容名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容名稱**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[內容名稱](/help/reporting/dimensions/content-name.md)。*

>[!ENDSHADEBOX]

內容名稱變數是內容的可讀取標題（例如，`"Blinding Light"`）。 這是選用專案，但強烈建議使用。 在XDM結構描述中，它將對應到`friendlyName` （不是`name`；`name`儲存內容識別碼）。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.friendlyName` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.friendlyName` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`friendlyName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "Blinding Light",
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

將人類可讀的名稱做為第一個(`name`)引數傳遞給`createMediaObject`。 第二個引數是內容ID。

```swift
let mediaObject = Media.createMediaObjectWith(name: "Blinding Light",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

將人類可讀的名稱做為第一個(`name`)引數傳遞給`createMediaObject`。 第二個引數是內容ID。

```kotlin
var mediaInfo = Media.createMediaObject("Blinding Light",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

呼叫`createMediaSession`時在`xdm.mediaCollection.sessionDetails`內設定`friendlyName`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "Blinding Light",
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

呼叫`xdm.mediaCollection.sessionDetails`內有`friendlyName`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "friendlyName": "Blinding Light",
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

將人類可讀的名稱作為第一個引數傳遞給`ADB.Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "Blinding Light",    // name (friendly name)
  "video-123",              // media ID
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

將人類可讀的名稱作為第一個引數傳遞給`ADBMobile.media.createMediaObject`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "Blinding Light",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

將人類可讀的名稱作為第一個引數傳遞給`adb_media_init_mediainfo`：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Blinding Light", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.name`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.name": "Blinding Light"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
