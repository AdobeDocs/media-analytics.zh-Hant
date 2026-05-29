---
title: 廣告插播名稱
description: 設定上層廣告插播的易記名稱。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 6%

---


# 廣告插播名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**廣告插播名稱**變數的資料集合。 如需對應的報表維度，請參閱[Pod名稱](/help/reporting/dimensions/pod-name.md)。*

>[!ENDSHADEBOX]

廣告插播名稱變數是廣告插播的易記名稱（例如，`"pre-roll"`、`"mid-roll-1"`、`"post-roll"`）。 值是在廣告插播物件上設定，而非個別廣告。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.ad.podFriendlyName` |
| **XDM集合欄位** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.ad.podFriendlyName` |
| **必要** | 是（行動SDK）；否（Edge、媒體收集API） |
| **與**&#x200B;一起傳送 | [廣告插播開始](/help/implementation/events/ads/ad-break-start.md)，廣告關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫`media.adBreakStart`的[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.advertisingPodDetails`內設定`friendlyName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將廣告插播名稱作為第一個(`name`)引數傳遞至`createAdBreakObject`，然後在廣告開始事件之前追蹤廣告插播開始事件。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

將廣告插播名稱作為第一個(`name`)引數傳遞至`createAdBreakObject`，然後在廣告開始事件之前追蹤廣告插播開始事件。

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

呼叫`media.adBreakStart`的`sendMediaEvent`時，在`xdm.mediaCollection.advertisingPodDetails`中設定`friendlyName`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.advertisingPodDetails`內有`friendlyName`的[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
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

將廣告插播名稱作為第一個引數傳遞給`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

將廣告插播名稱作為第一個引數傳遞給`ADBMobile.media.createAdBreakObject`：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB 媒體收集API]

在`adBreakStart` POST要求的`params`物件中包含`media.ad.podFriendlyName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
