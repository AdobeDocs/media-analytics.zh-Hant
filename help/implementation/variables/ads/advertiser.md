---
title: 廣告商
description: 設定每個廣告中精選的公司或品牌。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# 廣告商

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告商**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[廣告商](/help/reporting/dimensions/advertiser.md)。*

>[!ENDSHADEBOX]

廣告商變數是廣告中精選的公司或品牌（例如，`"Ford"`或`"Coca-Cola"`）。 使用變數來劃分廣告商的參與和完成。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.advertiser` |
| **XDM集合欄位** | [`mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.advertiser` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [廣告開始](/help/implementation/events/ads/ad-start.md)，廣告關閉 |

## Web SDK

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`mediaCollection.advertisingDetails`內設定`advertiser`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

將廣告商作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.ADVERTISER`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

呼叫`media.adStart`的`sendMediaEvent`時，在`mediaCollection.advertisingDetails`中設定`advertiser`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

呼叫`mediaCollection.advertisingDetails`內有`advertiser`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

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
          "podPosition": 0,
          "advertiser": "Ford"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.AdMetadataKeys.Advertiser`在`contextData`物件中傳遞廣告商：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

在`params`物件中包含`media.ad.advertiser`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
