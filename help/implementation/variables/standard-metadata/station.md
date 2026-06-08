---
title: 電台
description: 設定音訊廣播內容的廣播電台名稱或ID。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 9%

---


# 電台

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**站台**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[工作站](/help/reporting/dimensions/station.md)。*

>[!ENDSHADEBOX]

站台變數是廣播音訊內容的廣播電台名稱或ID （例如，`"NPR"`或`"WXYZ-FM"`）。 用它來比較聯合網路中跨站台的參與度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.station` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.station` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`station`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        station: "NPR"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將站台作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.AudioMetadataKeys.STATION`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

將站台作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.AudioMetadataKeys.STATION`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`設定`sessionDetails`內的`station`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "station": "NPR"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`station`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "station": "NPR"
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

使用`ADB.Media.AudioMetadataKeys.Station`傳遞`contextData`物件中的站台：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Station] = "NPR";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在呼叫`trackSessionStart`之前，使用`ADBMobile.media.AudioMetadataKeys.STATION`在媒體物件的`StandardMediaMetadata`屬性中設定站台名稱：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "NPR";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在呼叫`mediaTrackSessionStart`之前，使用`MEDIA_AudioMetadataKeySTATION`在媒體物件的標準中繼資料中設定站台名稱：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeySTATION] = "NPR"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.station`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.station": "NPR"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
