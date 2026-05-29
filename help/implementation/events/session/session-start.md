---
title: 工作階段開始
description: 代表媒體工作階段開始，並取得所有後續事件所需的工作階段ID。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 5%

---


# 工作階段開始

工作階段開始事件會開啟媒體追蹤工作階段。 此事件必須是任何播放所傳送的第一個事件。 回應會傳回相同工作階段的所有後續事件都必須包含的工作階段ID。

如果&#x200B;**在10分鐘內未收到任何事件**，或是&#x200B;**在30分鐘內沒有播放點移動**，工作階段會自動過期。 如果工作階段過期，您必須再次呼叫工作階段開始以取得新的工作階段ID。

* **必要條件**：無；永遠是第一個事件
* **關聯的量度**： [[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.sessionStart"`和必要的`sessionDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)。 回應包含`handle[].payload[].sessionId`中的工作階段識別碼（型別`media-analytics:new-session`）。 儲存這個值，並在所有後續事件中以`sessionID`的形式傳遞。

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
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

使用媒體物件和選擇性中繼資料呼叫`trackSessionStart`。

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

使用媒體物件和選擇性中繼資料呼叫`trackSessionStart`。

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku]

使用必要的階段作業詳細資料呼叫`createMediaSession`：

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
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點。 回應包含`handle[].payload[].sessionId`中的工作階段識別碼（型別`media-analytics:new-session`）。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用使用`ADB.Media.createMediaObject`建立的媒體物件來呼叫`trackSessionStart`：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

使用使用`ADBMobile.media.createMediaObject`建立的媒體物件來呼叫`trackSessionStart`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "video-123",                        // name
  "video-id-123",                     // media ID
  128,                                // length (seconds)
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);

ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒體收集API]

傳送`sessionStart`張貼至[工作階段端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。 回應`Location`標頭包含要用於所有後續事件要求的工作階段識別碼。

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```

>[!ENDTABS]

## 繼續工作階段

恢復先前關閉的工作階段時（例如，在跨裝置切換後或應用程式恢復儲存的播放狀態後），請在工作階段開始時設定恢復旗標。 這會導致Analytics增加[[!UICONTROL 內容繼續]](/help/reporting/metrics/content-resumes.md)，而非[[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md)。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

新增`hasResume: true`至`sessionDetails`：

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
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

呼叫`trackSessionStart`之前，在媒體物件上設定`resumed`索引鍵：

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

mediaObject[MediaConstants.MediaObjectKey.resumed] = true
tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

呼叫`trackSessionStart`之前，在媒體物件上設定`RESUMED`索引鍵：

```kotlin
val mediaObject = Media.createMediaObject("video-123", "video-id-123", 128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

mediaObject[Media.MediaObjectKey.RESUMED] = true
tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku]

新增`"hasResume": true`至`sessionDetails`：

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
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

新增`"hasResume": true`至`sessionDetails`：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

在媒體物件上設定`MediaResumed`索引鍵：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video
);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;
tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

在媒體物件上設定`MediaResumed`索引鍵：

```javascript
var mediaObject = ADBMobile.media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video
);

mediaObject[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaObject, null);
```

>[!TAB 媒體收集API]

將`"media.resume": true`新增至`params`物件：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123",
    "media.resume": true
  }
}
```

>[!ENDTABS]
