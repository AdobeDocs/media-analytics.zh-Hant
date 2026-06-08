---
title: 創作 URL
description: 設定每個廣告的廣告創意URL。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 10%

---


# 創作 URL

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**Creative URL**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[Creative URL](/help/reporting/dimensions/creative-url.md)。*

>[!ENDSHADEBOX]

創意URL變數是廣告創意的URL。 當URL本身對分析有意義時（例如，區分CDN路徑或創意版本），請使用變數來追蹤每個創意內容的資產位置。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.creativeURL` |
| **XDM集合欄位** | [`xdm.mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.creativeURL` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [廣告開始](/help/implementation/events/ads/ad-start.md)，廣告關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.advertisingDetails`內設定`creativeURL`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將創意URL作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.CREATIVE_URL`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

將創意URL作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.CREATIVE_URL`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

呼叫`media.adStart`的`sendMediaEvent`時，在`xdm.mediaCollection.advertisingDetails`中設定`creativeURL`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.advertisingDetails`內有`creativeURL`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
        },
        "sessionID": "{sid}",
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

使用`ADB.Media.AdMetadataKeys.CreativeUrl`在`contextData`物件中傳遞創意URL：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

使用標準廣告中繼資料物件中的`ADBMobile.media.AdMetadataKeys.CREATIVE_URL`設定創意URL：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

使用標準廣告中繼資料物件中的`MEDIA_AdMetadataKeyCREATIVE_URL`設定創意URL：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.ad.creativeURL`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
