---
title: 串流媒體收集 API - 事件要求端點
description: 什麼是Media Collection API事件要求端點引數和回應？
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# 事件要求{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI 參數

`sid`：從[工作階段要求](mc-api-sessions-req.md) 傳回的工作階段 ID。

## 要求內文

要求內文必須是 JSON，而且結構必須與以下範例要求內文相同：

```json
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

如需有效事件型別和每個SDK實作範例的清單，請參閱[事件概觀](/help/implementation/events/overview.md)。

>[!IMPORTANT]
>
>***廣告追蹤 -**&#x200B;您只能追蹤`adBreak`* 內的廣告。
>
>如果廣告周圍缺少 `adBreakStart` 和 `adBreakComplete`「書擋」，系統將會忽略 `adStart` 和 `adComplete` 事件，並將對應的廣告持續時間視為主要內容持續時間來追蹤。 這可能會對 Adobe Analytics 提供的彙總資料產生重大影響。

## 回應

```text
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
| **204** | **沒有內容。** <br/><br/>心率呼叫成功。 | 不適用 |
| **400** | **錯誤請求。** <br/><br/>要求的格式不正確。 | 如需要求類型，請查看 [JSON 驗證結構](mc-api-json-validation.md)。 |
| **404** | 找不到&#x200B;**。** <br/><br/>在後端服務找不到媒體工作階段的工作階段識別碼。 | 用戶端應用程式應使用[工作階段要求](mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **410** | **已過期。** <br/><br/>在後端服務找到媒體工作階段，但使用者端無法回報相關活動。 | 用戶端應用程式應使用[工作階段要求](mc-api-sessions-req.md) API，建立其他媒體工作階段並回報相關追蹤。 |
| **500** | **伺服器錯誤** | 不適用 |
