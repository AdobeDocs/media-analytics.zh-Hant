---
title: 創作者
description: 設定內容的建立者或製作工作室。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 17%

---


# 創作者

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**Originator**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[建立者](/help/reporting/dimensions/originator.md)。*

>[!ENDSHADEBOX]

創作者變數是內容的建立者或製作工作室（例如，`"Warner Brothers"`、`"Sony"`或`"Disney"`）。 用它來比較內容擁有者或權利持有者的參與情形。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.originator` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`originator`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        originator: "Warner Brothers"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

將建立者當作HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.ORIGINATOR`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`設定`sessionDetails`內的`originator`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "originator": "Warner Brothers"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`originator`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "originator": "Warner Brothers"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.Originator`傳遞`contextData`物件中的建立者：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Originator] = "Warner Brothers";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.originator`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.originator": "Warner Brothers"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
