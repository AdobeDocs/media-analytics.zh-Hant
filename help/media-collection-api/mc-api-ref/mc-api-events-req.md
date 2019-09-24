---
seo-title: 事件要求
title: 事件要求
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 事件要求{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI參數

`sid`:會話ID從「會話」請求 [中傳回。](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## 要求內文

The request body must be JSON, and must have the same structure as this sample request body:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (必要)
   * `playhead` - 必須以秒為單位，不過可以是浮點數。
   * `ts` - 時間戳記；必須以毫秒為單位。
* `eventType` (必要)
* `params` (可選)
* `customMetadata` (可選；僅傳送及 `adStart` 事件 `chapterStart` 類型)
* `qoeData` (可選)

For a list of valid event types for this release, see [Event types and descriptions.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***廣告追蹤**-您只能追蹤廣告內`adBreak`*&#x200B;部。
>
>如果廣告周圍缺少 `adBreakStart` 和 `adBreakComplete`「書擋」，系統將會忽略 `adStart` 和 `adComplete` 事件，並將對應的廣告持續時間視為主要內容持續時間來追蹤。這可能會對 Adobe Analytics 提供的彙總資料產生重大影響。

## 回應

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP 回應代碼

| HTTP 回應代碼 | 說明 | 用戶端動作項目 |
|---|---|---|
| **204** | **沒有內容.**<br/><br/> 心率呼叫成功。 | 不適用 |
| **400** | **Bad Request。**<br/><br/> 要求格式錯誤。 | 如需要求類型，請查看 [JSON 驗證結構](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)。 |
| **404** | **找不到.** 在 <br/><br/>後端服務中找不到媒體會話的會話ID。 | 用戶端應用程式應使用[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **410** | **Gone.** 在後 <br/><br/>端服務中找到媒體會話，但客戶端無法再報告其活動。 | 用戶端應用程式應使用[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **500** | **伺服器錯誤** | 不適用 |

