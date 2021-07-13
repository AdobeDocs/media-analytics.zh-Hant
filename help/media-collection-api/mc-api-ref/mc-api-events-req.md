---
title: 串流媒體收集API事�件要求端點
description: '"什麼是Media Collection API事件要求端點參數和回應？"'
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 92%

---

# 事件要求{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI 參數

`sid`: 從[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)傳回的工作階段 ID。

## 要求內文

要求內文必須是 JSON，而且結構必須與以下範例要求內文相同:

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
* `customMetadata` (選用；只能連同 `adStart` 和 `chapterStart` 事件類型一起傳送)
* `qoeData` (可選)

如需該版本的有效事件類型清單，請參閱[事件類型和說明](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)。

>[!IMPORTANT]
>
>***廣告追蹤 -**您只能追蹤`adBreak`* 內的廣告。
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
| **204** | **沒有內容。**<br/><br/> 心率呼叫成功。 | 不適用 |
| **400** | **Bad Request。**<br/><br/> 要求格式錯誤。 | 如需要求類型，請查看 [JSON 驗證結構](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)。 |
| **404** | **找不到。** <br/><br/>在後端服務找不到媒體工作階段的工作階段 ID。 | 用戶端應用程式應使用[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **410** | **已過期。** <br/><br/>在後端服務找到媒體工作階段，但用戶端無法回報相關活動。 | 用戶端應用程式應使用[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **500** | **伺服器錯誤** | 不適用 |
