---
title: 內容繼續
description: 標幟工作階段以繼續先前中斷的播放，讓後端會計為內容繼續事件。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# 內容繼續

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**內容繼續**變數的資料集合。 檢視[[!UICONTROL 對應報表量度的內容履歷]](/help/reporting/metrics/content-resumes.md)。*

>[!ENDSHADEBOX]

內容繼續變數會標籤繼續先前中斷之播放的工作階段。 將其設定在`media.sessionStart`，以便後端計算工作階段的[[!UICONTROL 內容繼續]](/help/reporting/metrics/content-resumes.md)事件，並將其從新資料流計數中排除。 對於直接API和Edge API實作，使用者端負責偵測恢復的工作階段（例如，在緩衝、暫停或超過30分鐘的延遲後）並相應地設定此標幟。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.resume` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | 不適用 |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md) |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫繼續工作階段的[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，將`xdm.mediaCollection.sessionDetails`內的`hasResume`設為`true`：

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
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

在`trackSessionStart`上傳遞恢復旗標，做為媒體物件的選擇性設定組合的一部分。 使用`MediaConstants.MediaObjectKey.RESUMED`金鑰。

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

在`trackSessionStart`上傳遞恢復旗標，做為媒體物件的選擇性設定組合的一部分。 使用`MediaConstants.MediaObjectKey.RESUMED`金鑰。

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

呼叫繼續工作階段的`createMediaSession`時，在`xdm.mediaCollection.sessionDetails`內將`hasResume`設為`true`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點，其中`xdm.mediaCollection.sessionDetails`內的`hasResume`設定為`true`：

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

呼叫`trackSessionStart`之前，在媒體資訊物件上設定`RESUMED`鍵：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

呼叫`trackSessionStart`之前，在媒體資訊物件上設定`MediaResumed`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.resume`：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
