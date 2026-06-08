---
title: 廣告載入型別
description: 設定串流工作階段的廣告載入型別。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 3%

---


# 廣告載入型別

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告載入型別**&#x200B;變數的資料集合。 檢視對應報表維度的[廣告載入](/help/reporting/dimensions/ad-load-type.md)。*

>[!ENDSHADEBOX]

廣告載入型別變數會識別工作階段開始時載入的廣告型別。 此值由貴組織的內部廣告傳遞系統定義，不受標準分項清單的限制。 您可以使用對實作有意義的任何字串，例如`"linear"`、`"dynamic"`或`"programmatic"`。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.adLoad` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.adLoad` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`createMediaSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/createmediasession)時，在`xdm.mediaCollection.sessionDetails`內設定`adLoad`：

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將廣告載入型別作為字典引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.AD_LOAD`。

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

將廣告載入型別當做HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.AD_LOAD`。

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`設定`sessionDetails`內的`adLoad`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.sessionDetails`內有`adLoad`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

使用`ADB.Media.VideoMetadataKeys.AdLoad`在`contextData`物件中傳遞廣告載入型別：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在呼叫`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.AD_LOAD`在媒體物件的`StandardMediaMetadata`屬性中設定廣告載入型別：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在呼叫`mediaTrackSessionStart`之前，使用`MEDIA_VideoMetadataKeyAD_LOAD`在媒體物件的標準中繼資料中設定廣告載入型別：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyAD_LOAD] = "linear"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.adLoad`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
