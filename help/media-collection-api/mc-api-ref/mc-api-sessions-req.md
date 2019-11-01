---
title: 工作階段要求
description: null
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 工作階段要求{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI參數

無

## 要求內文

請求內文必須是JSON，且必須具有與此範例請求內文相同的結構：

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (必要)
   * `playhead` - 必須以秒為單位，不過可以是浮點數。
   * `ts` - 時間戳記；必須以毫秒為單位。
* `eventType` (必要)

   **有效值：**`sessionStart`
* `params` (必要)
* `customMetadata` (可選)
* `qoeData` (可選)

## 回應

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header —— 部 `/api/v1/` 件提供API版本。 後面的部 `[…]sessions/` 件是會話ID。

## 回應代碼

| HTTP 回應代碼 | 說明 |
|---|---|
| 201 | Session created |
| 400 | Bad Request |
| 500 | Server error |

