---
title: 工作階段結束
description: 當檢視器放棄內容時，立即關閉媒體工作階段。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---


# 工作階段結束

工作階段結束事件會立即且不可撤銷地關閉媒體追蹤工作階段。 工作階段結束是硬性關閉 — 一旦傳送，工作階段就會終止，且無法在其下追蹤進一步事件。 只有在您確定不會發生其他事件時（例如當播放器損毀或頁面解除安裝時），才使用「工作階段結束」。 在多數情況下，允許工作階段自然過期會比較安全，而不用冒截斷仍可能抵達之事件的風險。 如果檢視器完成內容，請改為呼叫[工作階段完成](session-complete.md)。

如果沒有明確的工作階段結束，工作階段會在沒有事件的10分鐘或播放點沒有移動的30分鐘後自動關閉。

>[!NOTE]
>
>您可以安全地為相同工作階段呼叫工作階段結束多次。 後端會關閉第一個事件的工作階段，並自動捨棄該工作階段ID的所有後續事件，包括第二個工作階段結束。 您不需要在競爭狀況下防止重複呼叫，例如30分鐘逾時在檢視器關閉播放器的同時到期。

* **必要條件**： [工作階段開始](session-start.md)
* **關聯的量度**：無

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.sessionEnd"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

當檢視器關閉播放器或導覽離開時，請呼叫`trackSessionEnd`。

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

當檢視器關閉播放器或導覽離開時，請呼叫`trackSessionEnd`。

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Roku]

與`eventType: "media.sessionEnd"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

當檢視器關閉播放器或導覽離開時呼叫`trackSessionEnd`：

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

當檢視器關閉播放器或導覽離開時呼叫`trackSessionEnd`：

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB 媒體收集API]

傳送`sessionEnd`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]
