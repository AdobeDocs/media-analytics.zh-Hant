---
title: 行銷活動 ID
description: 設定每個廣告的行銷活動識別碼，以便行銷活動可以彙總參與度。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 10%

---


# 行銷活動 ID

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**促銷活動識別碼**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[促銷活動識別碼](/help/reporting/dimensions/campaign-id.md)。*

>[!ENDSHADEBOX]

行銷活動ID變數可識別創意所屬的廣告行銷活動。 可接受任何字串值（通常是廣告伺服器平台的促銷活動ID）。 使用變數，可在共用行銷活動的多個創意人員之間彙總參與度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.campaign` |
| **XDM集合欄位** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.campaign` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [廣告開始](/help/implementation/events/ads/ad-start.md)，廣告關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.advertisingDetails`內設定`campaignID`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將行銷活動ID作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.CAMPAIGN_ID`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

將行銷活動ID作為HashMap引數中的中繼資料索引鍵傳遞給`trackEvent(AdStart)`。 使用`MediaConstants.AdMetadataKeys.CAMPAIGN_ID`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

呼叫`media.adStart`的`sendMediaEvent`時，在`xdm.mediaCollection.advertisingDetails`中設定`campaignID`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.advertisingDetails`內有`campaignID`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)端點：

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
          "campaignID": "fall-2024"
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

使用`ADB.Media.AdMetadataKeys.CampaignId`在`contextData`物件中傳遞行銷活動ID：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

使用標準廣告中繼資料物件中的`ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID`設定促銷活動ID：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.ad.campaignId`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
