---
title: Ping
description: 傳送心率以保持媒體工作階段作用中並定期追蹤播放進度。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Ping

Ping事件是心率，可讓工作階段持續運作並追蹤播放進度。 在播放過程中，透過計時器傳送檔案。

* **主要內容**：開始播放後第一個ping 10秒，之後每10秒一次
* **廣告內容**：在廣告追蹤期間每1秒

請勿在Ping要求內文中包含`params`物件。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**：無

## Web SDK

排程與`eventType: "media.ping"`的週期性`sendEvent`呼叫。 將`playhead`更新至每次呼叫的目前播放位置：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## Mobile SDK

行動SDK會自動傳送Ping事件。 不需要明確呼叫。

## Roku (BrightScript)

排程與`eventType: "media.ping"`的週期性`sendMediaEvent`呼叫。 將`playhead`更新至每次呼叫的目前播放位置：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## Media Edge API

呼叫計時器上的[ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/)端點。 Adobe建議在主要播放開始後第一個ping 10秒、之後每10秒一次，以及在廣告追蹤期間每1秒一次：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Media SDK會自動傳送Ping事件。 不需要明確呼叫。

## Media Collection API

傳送`ping` POST至計時器上的[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。 不要包含`params`物件：

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
