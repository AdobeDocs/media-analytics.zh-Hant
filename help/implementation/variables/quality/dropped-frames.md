---
title: 掉格
description: 設定QoE物件上掉格的執行計數，讓後端可以報告掉格品質。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 5%

---


# 掉格

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**掉格**&#x200B;變數的資料集合。 檢視對應報表維度和量度的[掉格](/help/reporting/dimensions/dropped-frames.md)。*

>[!ENDSHADEBOX]

dropped frames變數是播放器在工作階段期間捨棄的畫面執行計數。 將其設定在QoE物件上，並在播放器回報新資料掉格時更新值。 後端會在工作階段關閉時報告最新值。

>[!NOTE]
>
>請一律傳遞截至該時間為止整個工作階段的&#x200B;**累積總計**&#x200B;個掉格，而非每個間隔差值。 如果您在更新之間將值重設為`0`，則後端會接收`0`作為最終值，並報告工作階段的零掉格，無論之前實際掉格為何。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.qoe.droppedFrameCount` |
| **XDM集合欄位** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | 品質事件（[位元速率變更](/help/implementation/events/playback/bitrate-change.md)，[緩衝開始](/help/implementation/events/playback/buffer-start.md)，[錯誤](/help/implementation/events/error.md)），工作階段關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.qoeDataDetails`內設定`droppedFrames`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

將捨棄的影格作為第四個引數傳遞給`createQoEObject`。 在任何品質事件引發之前更新追蹤器。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

將捨棄的影格作為第四個引數傳遞給`createQoEObject`。 在任何品質事件引發之前更新追蹤器。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

呼叫`sendMediaEvent`時在`xdm.mediaCollection.qoeDataDetails`內設定`droppedFrames`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

呼叫`xdm.mediaCollection.qoeDataDetails`內有`droppedFrames`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
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

將捨棄的影格作為第四個引數傳遞給`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

將累積掉格計數作為第四個引數傳入`ADBMobile.media.createQoSObject`並更新追蹤器：

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB 媒體收集API]

在`params`物件中包含`media.qoe.droppedFrames`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
