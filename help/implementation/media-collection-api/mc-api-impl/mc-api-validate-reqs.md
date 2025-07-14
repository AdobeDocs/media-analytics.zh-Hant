---
title: 驗證事件要求
description: 了解如何使用 JSON 驗證結構來驗證事件要求。
uuid: 1fc92f21-b510-4c96-8ea2-47e819f4a96e
exl-id: a78739da-9fc9-42e3-9181-1887fb3dd357
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 100%

---

# 驗證事件要求{#validating-event-requests}

每種事件類型的 JSON 要求內文，都會在後端以 JSON 結構加以驗證。當 API 呼叫驗證失敗時，系統會在 HTTP 回應內文中填入錯誤訊息。

每種事件類型的 JSON 驗證結構均可公開存取，請前往：`{uri}/api/v1/schemas/{eventType}` (例如 `{uri}/api/v1/schemas/sessionEnd`)。JSON 驗證結構是判斷每種事件類型之正確要求內容參數的絕對可信來源。

例如，`sessionStart` 驗證結構之要求的回應將與以下範例相似 (稍微調整格式以利閱讀)：

```
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Thu, 18 Jan 2018 15:44:50 GMT
Content-Type: application/json
Content-Length: 2716
Connection: keep-alive

{
  "$schema":"https://json-schema.org/draft-04/schema#",
  "id":"https://alpha.hb-api.omtrdc.net/api/v1/schemas/sessionStart",
  "definitions":
  {
    "playerTime":
    {
      "type":"object","properties":
      {
        "playhead":
        {"type":"number"},
        "ts":
        {"type":"integer"}
      },
      "required":["playhead","ts"],
      "additionalProperties":false
    },
    "eventType":
    {
      "type":"string",
      "enum":[
        "sessionStart",
        "play",
        "ping",
        "bufferStart",
        "pauseStart",
        "sessionComplete",
        "bitrateChange",
        "error",
        "adBreakStart",
        "adBreakComplete",
        "adStart",
        "adComplete",
        "adSkip",
        "sessionEnd"
      ]
    },
    "qoeData":
    {
      "type":"object","properties":
      {
        "media.qoe.bitrate":
        {"type":"integer"},
        "media.qoe.droppedFrames":
        {"type":"integer"},
        "media.qoe.framesPerSecond":
        {"type":"integer"},
        "media.qoe.timeToStart":
        {"type":"integer"}
      },
      "required":[],
      "additionalProperties":false
    },
    "customMetadata":
    {
      "type":"object",
      "patternProperties":
      {
        "^[a-zA-Z0-9_\\.]+$":
        {"type":"string"}
      },
      "additionalProperties":false
    },
    "sessionStart":
    {
      "properties":
      {
        "eventType":
        {"type":"string","enum":["sessionStart"]},
        "playerTime":
        {"$ref":"#/definitions/playerTime"},
        "params":
        {"type":"object",
          "properties":
          {
            "appInstallationId":
            {"type":"string"},
            "analytics.trackingServer":
            {"type":"string"},
            "analytics.reportSuite":
            {"type":"string"},
            <...>
            "visitor.marketingCloudOrgId"],
            "additionalProperties":false
          },
          "customMetadata":
          {"$ref":"#/definitions/customMetadata"},
          "qoeData":
          {"$ref":"#/definitions/qoeData"}
        },
        "required":["eventType","playerTime","params"],
        "additionalProperties":false
      }
    },
    "type":"object","$ref":"#/definitions/sessionStart"
  }
}
```

>[!NOTE]
>
>由於無法在收集層取得工作階段內容，因此無法進行工作階段層級驗證。
