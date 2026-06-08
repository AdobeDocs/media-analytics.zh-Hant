---
title: 媒體已下載的旗標
description: 將工作階段標示為已下載的離線播放，以便與串流工作階段分開報告。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---


# 媒體已下載的旗標

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**媒體下載旗標**變數的資料集合。 檢視對應報表維度的[下載的媒體](/help/reporting/dimensions/media-downloaded-flag.md)。*

>[!ENDSHADEBOX]

「媒體已下載」標幟指出工作階段是播放先前下載的離線內容，而非來自網際網路的即時資料流。 初始化追蹤器（行動SDK）時設定它，或將其納入`sessionStart`裝載（Edge /媒體收集API）。 使用此標幟在報告中將離線播放與串流工作階段分開。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.downloaded` |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.downloaded` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.sessionDetails`內將`isDownloaded`設為`true`：

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
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

使用`MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`建立追蹤器時，在追蹤器設定上設定下載內容標幟。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

使用`MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`建立追蹤器時，在追蹤器設定上設定下載內容標幟。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

呼叫`createMediaSession`時在`xdm.mediaCollection.sessionDetails`內將`isDownloaded`設為`true`：

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
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

在裝置返回上線後，呼叫[已下載](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded)端點，在`mediaDownloadedEvents`內批次處理完整的離線工作階段。 Adobe會自動將`isDownloaded`設定為`true`並指派工作階段ID；請勿在承載中包含任一工作階段。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

建立追蹤器之前，先在`ADB.MediaConfig`上設定`downloadedContent`：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

呼叫`trackSessionStart`之前，在媒體資訊物件上設定`MediaDownloaded`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaDownloaded] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Roku 2.x SDK不提供下載內容追蹤功能。 若要報告下載的媒體播放，請使用[Roku Edge SDK](/help/implementation/edge/roku.md)或[媒體收集API](/help/implementation/analytics-only/media-collection-api.md)。

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.downloaded`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
