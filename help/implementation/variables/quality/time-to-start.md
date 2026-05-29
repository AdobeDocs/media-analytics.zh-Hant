---
title: 開始時間
description: 設定播放器的啟動時間（以毫秒為單位），讓後端可以報告時間到第一個影格品質。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 6%

---


# 開始時間

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**開始時間**變數的資料集合。 如需對應的報表維度和量度，請參閱[[!UICONTROL 開始時間]](/help/reporting/dimensions/time-to-start.md)。*

>[!ENDSHADEBOX]

開始時間變數是播放器起始播放與第一個影格轉譯之間經過的時間，以毫秒為單位。 在工作階段開始事件引發之前，在QoE物件上設定它。 Adobe會以秒為單位儲存和報告值；傳遞毫秒，Adobe會在擷取時轉換。

>[!IMPORTANT]
>
>播放器開始轉譯內容框架後，請停止更新`timeToStart`。 此值可能會在初始緩衝或載入階段期間增加，但應視為從播放開始時刻起即已固定。 在第一個影格轉譯後繼續更新，會產生膨脹或不正確的[[!UICONTROL 開始時間]](/help/reporting/metrics/time-to-start.md)量度。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.qoe.timeToStart` |
| **XDM集合欄位** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.qoe.timeToStart` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md)，工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`media.sessionStart`的`xdm.mediaCollection.qoeDataDetails`中設定`timeToStart`：

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
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將啟動時間作為第二個引數(`startupTime`)傳遞給`createQoEObject`。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

將啟動時間作為第二個引數(`startupTime`)傳遞給`createQoEObject`。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

呼叫`createMediaSession`時，在`media.sessionStart`的`xdm.mediaCollection.qoeDataDetails`中設定`timeToStart`：

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
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.qoeDataDetails`內有`timeToStart`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)端點：

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
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
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

將開始時間作為第二個引數傳遞給`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

將啟動時間以毫秒為單位作為第二個引數(`startupTime`)傳遞至`ADBMobile.media.createQoSObject`並更新追蹤器：

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB 媒體收集API]

在`sessionStart`上的`params`物件中包含`media.qoe.timeToStart`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
