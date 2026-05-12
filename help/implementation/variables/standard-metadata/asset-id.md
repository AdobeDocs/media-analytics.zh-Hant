---
title: 資產 ID
description: 設定資產ID，此為媒體資產的穩定產業識別碼，例如EIDR或TMS/Gracenote ID。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 13%

---


# 資產 ID

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**資產識別碼**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[資產識別碼](/help/reporting/dimensions/asset-id.md)。*

>[!ENDSHADEBOX]

資產ID變數是基礎媒體資產的唯一識別碼（例如集數ID、電影ID或即時事件ID）。 通常取自中繼資料授權單位，例如EIDR、TMS/Gracenote或Rovi，但也接受專屬或內部ID。 當您需要比較可能將不同內容ID指派給相同基礎資產的分銷平台間的參與時，請使用它。

>[!NOTE]
>
>XDM集合欄位使用大寫`ID`： `assetID`。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.asset` |
| **XDM集合欄位** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 工作階段開始、工作階段關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.sessionDetails`內設定`assetID`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

將資產ID作為HashMap引數中的中繼資料索引鍵傳遞給`trackSessionStart`。 使用`MediaConstants.VideoMetadataKeys.ASSET_ID`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`設定`sessionDetails`內的`assetID`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.sessionDetails`內有`assetID`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.AssetId`傳遞`contextData`物件中的資產ID：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.assetId`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
