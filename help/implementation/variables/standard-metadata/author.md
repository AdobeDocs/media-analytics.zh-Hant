---
title: 作者
description: 設定內容的作者。 主要用於有聲書。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 9%

---


# 作者

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**作者**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[作者](/help/reporting/dimensions/author.md)。*

>[!ENDSHADEBOX]

作者變數是內容的作者（例如，`"Eleanor Clementine"`）。 主要用於有聲書，但也適用於其主機或製作人為相關歸因的播客。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.author` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.author` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`author`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        author: "Eleanor Clementine"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將作者作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.AudioMetadataKeys.AUTHOR`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

將作者作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.AudioMetadataKeys.AUTHOR`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`設定`sessionDetails`內的`author`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "author": "Eleanor Clementine"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`author`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "author": "Eleanor Clementine"
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

使用`ADB.Media.AudioMetadataKeys.Author`在`contextData`物件中傳遞作者：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Author] = "Eleanor Clementine";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在呼叫`trackSessionStart`之前，使用`ADBMobile.media.AudioMetadataKeys.AUTHOR`設定媒體物件之`StandardMediaMetadata`屬性中的作者：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在呼叫`mediaTrackSessionStart`之前，使用`MEDIA_AudioMetadataKeyAUTHOR`在媒體物件的標準中繼資料中設定作者：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyAUTHOR] = "Eleanor Clementine"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.author`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.author": "Eleanor Clementine"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
