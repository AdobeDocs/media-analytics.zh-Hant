---
title: 每秒影格數
description: 在QoE物件上設定目前的影格速率，讓後端有品質報告的影格速率內容。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 7%

---


# 每秒影格數

每秒影格數變數是資料流的目前影格速率。 將其與位元速率和掉格一起設定在QoE物件上，讓後端擁有每個播放工作階段的完整品質內容。 Adobe Analytics不會自動建立影格速率的報表變數；如果您想要以報表的形式呈現，請建立自訂處理規則。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | 無（Adobe Analytics不會為影格速率指派保留的內容資料索引鍵） |
| **XDM集合欄位** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特徵** | 不適用 |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 品質事件（[位元速率變更](/help/implementation/events/playback/bitrate-change.md)，[緩衝開始](/help/implementation/events/playback/buffer-start.md)，[錯誤](/help/implementation/events/error.md)），工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.qoeDataDetails`內設定`framesPerSecond`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

將影格速率作為第三個引數(`fps`)傳遞給`createQoEObject`。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

將影格速率作為第三個引數(`fps`)傳遞給`createQoEObject`。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

呼叫`sendMediaEvent`時在`xdm.mediaCollection.qoeDataDetails`內設定`framesPerSecond`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.qoeDataDetails`內有`framesPerSecond`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

將影格速率作為第三個引數傳給`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

將影格速率作為第三個引數(`fps`)傳遞至`ADBMobile.media.createQoSObject`並更新追蹤器：

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.qoe.framesPerSecond`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
