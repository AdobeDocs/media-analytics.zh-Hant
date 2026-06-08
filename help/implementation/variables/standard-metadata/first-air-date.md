---
title: 首播日期
description: 設定內容在電視上的首播日期。 Adobe建議使用YYYY-MM-DD格式。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 7%

---


# 首播日期

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**首播日期**變數的資料收集。 如需對應的報表維度，請參閱[首播日期](/help/reporting/dimensions/first-air-date.md)。*

>[!ENDSHADEBOX]

第一個播放日期變數是內容在電視上的首播日期。 接受任何日期格式，但Adobe建議使用`YYYY-MM-DD`以保持一致性。 用它來比較新版本與目錄內容的參與度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.airDate` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.airDate` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內設定`firstAirDate`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstAirDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將第一次播放日期作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

將第一次播放日期作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`設定`sessionDetails`內的`firstAirDate`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstAirDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`firstAirDate`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "firstAirDate": "2016-01-25"
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

使用`ADB.Media.VideoMetadataKeys.FirstAirDate`傳遞`contextData`物件中的第一個播放日期：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在呼叫`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE`設定媒體物件`StandardMediaMetadata`屬性中的第一次播放日期：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在呼叫`mediaTrackSessionStart`之前，使用`MEDIA_VideoMetadataKeyFIRST_AIR_DATE`設定媒體物件之標準中繼資料中的首次播放日期：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyFIRST_AIR_DATE] = "2016-01-25"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.firstAirDate`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstAirDate": "2016-01-25"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
