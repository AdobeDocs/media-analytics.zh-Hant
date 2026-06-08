---
title: 網站 ID
description: 設定每個廣告的廣告網站ID以啟用依廣告位置網站劃分。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 10%

---


# 網站 ID

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**網站識別碼**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[網站ID](/help/reporting/dimensions/site-id.md)。*

>[!ENDSHADEBOX]

網站ID變數可識別廣告網站。 可接受任何字串值（通常是來自廣告伺服器平台的ID）。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.site` |
| **XDM集合欄位** | [`xdm.mediaCollection.advertisingDetails.siteID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.site` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [廣告開始](/help/implementation/events/ads/ad-start.md)，廣告關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.advertisingDetails`內設定`siteID`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        siteID: "site-42"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將網站ID作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.SITE_ID`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

將網站ID作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.SITE_ID`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

呼叫`media.adStart`的`sendMediaEvent`時，在`xdm.mediaCollection.advertisingDetails`中設定`siteID`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "siteID": "site-42"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.advertisingDetails`內有`siteID`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

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
          "siteID": "site-42"
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

使用`ADB.Media.AdMetadataKeys.SiteId`傳遞`contextData`物件中的網站識別碼：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.SiteId] = "site-42";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

在標準廣告中繼資料物件中使用`ADBMobile.media.AdMetadataKeys.SITE_ID`設定網站ID：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "site-42";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

在標準廣告中繼資料物件中使用`MEDIA_AdMetadataKeySITE_ID`設定網站ID：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeySITE_ID] = "site-42"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.ad.siteId`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.siteId": "site-42"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
