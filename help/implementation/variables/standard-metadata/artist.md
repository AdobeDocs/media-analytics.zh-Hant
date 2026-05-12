---
title: 藝術家
description: 設定音訊內容的演出藝人名稱。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 16%

---


# 藝術家

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**藝人**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[藝人](/help/reporting/dimensions/artist.md)。*

>[!ENDSHADEBOX]

演出者變數是音訊內容演出演出者的名稱（例如，`"Crested Larks"`）。 將其用於音樂或播客工作階段，以中斷執行者的參與。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.artist` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`artist`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        artist: "Crested Larks"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

將演出者名稱作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.AudioMetadataKeys.ARTIST`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`設定`sessionDetails`內的`artist`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "artist": "Crested Larks"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`artist`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "artist": "Crested Larks"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.AudioMetadataKeys.Artist`在`contextData`物件中傳遞演出者：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Artist] = "Crested Larks";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.artist`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.artist": "Crested Larks"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
