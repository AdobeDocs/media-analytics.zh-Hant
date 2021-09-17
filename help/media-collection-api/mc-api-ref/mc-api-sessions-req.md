---
title: 串流媒體收集API — 工作階段要求端點
description: 「媒體收集API工作階段要求端點參數和回應為何？」
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ef881900766be773256e2732953f7b63c5d488fa
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 46%

---

# 工作階段要求{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI 參數

無

## 要求內文

要求內文必須是 JSON，而且結構必須與以下範例要求內文相同:

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
   * `playhead`  — 如果內容為即時，播放點必須是當天的第二秒，0  &lt;>如果已記錄內容，播放點必須是內容的目前秒數，0 &lt;=播放點&lt;內容長度。 值可以是浮點數。
   * `ts`  — 時間戳記；必須以毫秒為單位；協調的世界時間(UTC)。
* `eventType` (必要)

   **有效值:** `sessionStart`
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

`Location:` 標頭 - `/api/v1/` 部分提供 API 版本。`[…]sessions/` 後的部分則為工作階段 ID。

## 回應代碼

| HTTP 回應代碼 | 說明 |
|---|---|
| 201 | Session created |
| 400 | Bad Request |
| 500 | Server error |
