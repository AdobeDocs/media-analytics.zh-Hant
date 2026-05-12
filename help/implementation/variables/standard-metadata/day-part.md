---
title: 時段
description: 設定廣播或播放內容時的當天時段（上午、下午、黃金時段、深夜）。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 13%

---


# 時段

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**天部分**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[日期部分](/help/reporting/dimensions/day-part.md)。*

>[!ENDSHADEBOX]

日部分變數是廣播或播放內容時的當日時段（例如，`"Morning"`、`"Afternoon"`、`"Primetime"`或`"Late Night"`）。 可接受任何字串。 用它來比較不同日時段、不同檢視者當地時區的參與度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.dayPart` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`dayPart`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        dayPart: "Primetime"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

將日期部分作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.DAY_PART`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`設定`sessionDetails`內的`dayPart`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "dayPart": "Primetime"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`dayPart`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "dayPart": "Primetime"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.DayPart`傳遞`contextData`物件中的日部分：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.dayPart`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.dayPart": "Primetime"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
