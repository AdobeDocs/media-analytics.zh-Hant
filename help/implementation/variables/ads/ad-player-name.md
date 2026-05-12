---
title: 廣告播放器名稱
description: 設定轉譯廣告之播放器的名稱。 廣告播放器可以和主要內容播放器不同。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 11%

---


# 廣告播放器名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告播放器名稱**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[廣告播放器名稱](/help/reporting/dimensions/ad-player-name.md)。*

>[!ENDSHADEBOX]

廣告播放器名稱變數會識別轉譯了每個廣告的播放器（例如，`"Freewheel"`、`"Google IMA"`）。 伺服器端廣告插入服務連結廣告時，廣告播放器可能會與主要內容播放器不同。 使用此變數可比較不同廣告服務棧疊的品質和完成情形。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.playerName` |
| **XDM集合欄位** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **必要** | 是 |
| **與**&#x200B;一起傳送 | 廣告開始、廣告關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingDetails`內設定`playerName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

將廣告播放器名稱作為中繼資料HashMap引數中的`MediaConstants.AdMetadataKeys.AD_PLAYER`索引鍵傳遞給`trackEvent(AdStart)`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

呼叫`media.adStart`的`sendMediaEvent`時，在`mediaCollection.advertisingDetails`中設定`playerName`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.advertisingDetails`內有`playerName`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.AdMetadataKeys.AdPlayer`在`contextData`物件中傳遞廣告播放器名稱：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

在`adStart` POST要求的`params`物件中包含`media.ad.playerName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
