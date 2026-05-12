---
title: 已驗證
description: 將工作階段標幟為已透過Adobe Pass驗證，因此會計入授權事件。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 15%

---


# 已驗證

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**已授權**&#x200B;變數的資料集合。 如需對應的報表量度，請參閱[已授權](/help/reporting/metrics/authorized.md)。*

>[!ENDSHADEBOX]

授權變數會標籤透過Adobe Pass / TV-Everywhere授權使用者的工作階段。 在確認授權時，將其設為`"TRUE"`；否則請將其保留為未設定。 與[MVPD](/help/implementation/variables/standard-metadata/mvpd.md)配對，以中斷提供者的驗證。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.pass.auth` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`authorized`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

將授權旗標作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.AUTHORIZED`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`設定`sessionDetails`內的`authorized`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`authorized`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "authorized": "TRUE"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.Authorized`在`contextData`物件中傳遞授權旗標：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.pass.auth`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
