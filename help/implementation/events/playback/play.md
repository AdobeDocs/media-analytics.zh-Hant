---
title: 播放
description: 表示媒體播放器已進入播放狀態。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 10%

---


# 播放

播放事件代表媒體播放器狀態已變更為播放。 在內容初次啟動時、自動播放時，以及播放器在暫停或緩衝後恢復時，均會傳送此訊息。 沒有個別的繼續事件；在[暫停開始](pause-start.md)或[緩衝開始](buffer-start.md)之後的播放事件可作為繼續事件。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**： [[!UICONTROL 內容開始]](/help/reporting/metrics/content-starts.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

與`eventType: "media.play"`通話[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

當媒體播放器開始或繼續播放時，呼叫`trackPlay`。

```swift
tracker.trackPlay()
```

>[!TAB Android]

當媒體播放器開始或繼續播放時，呼叫`trackPlay`。

```kotlin
tracker.trackPlay()
```

>[!TAB Roku]

與`eventType: "media.play"`通話`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

呼叫[播放](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

當媒體播放器開始或繼續播放時，呼叫`trackPlay`：

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

當媒體播放器開始或繼續播放時，呼叫`trackPlay`：

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB 媒體收集API]

傳送`play`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
