---
title: 錯誤
description: 表示媒體播放器發生錯誤。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 8%
---

# 錯誤

錯誤事件代表媒體播放器發生錯誤。 追蹤錯誤不會關閉工作階段。 如果錯誤導致無法繼續播放，請在錯誤事件後呼叫[工作階段結束](session/session-end.md)。

* **必要條件**： [工作階段開始](session/session-start.md)
* **關聯的量度**： [[!UICONTROL 錯誤影響的資料流]](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source`屬性只接受兩個值： `player` （源自媒體播放器的錯誤）和`external` （來自CDN或網路等外部來源的錯誤）。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.error"`和必要的`errorDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

使用錯誤識別碼字串呼叫`trackError`。

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

使用錯誤識別碼字串呼叫`trackError`。

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Roku Edge]

使用`eventType: "media.error"`和必要的`errorDetails`來呼叫`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge API]

使用必要的`errorDetails`呼叫[error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
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

使用錯誤識別碼字串呼叫`trackError`：

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

使用錯誤識別碼字串呼叫`trackError`：

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

使用錯誤識別碼和錯誤來源呼叫`mediaTrackError`。 使用播放器錯誤的`ERROR_SOURCE_PLAYER`常數：

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB 媒體收集API]

傳送`error`張貼至[事件端點](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
