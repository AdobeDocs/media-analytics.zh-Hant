---
title: 時間軸 3 - 章節
description: null
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 時間軸 3 - 章節 {#timeline-3-chapters}

## VOD、前段廣告、暫停、緩衝、檢視內容到結束為止


下圖說明播放頭時間軸和使用者動作的對應時間軸。 以下列出每項行動及其隨附要求的詳細資料。


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## 動作詳細資訊


### 操作1 —— 啟動會話 {#Action-1}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 自動播放或按下「播放」按鈕，開始載入視訊。 | 0 | 0 | `/api/v1/sessions` |

**實作詳細資訊**

此呼叫 _表示使用者播放視訊的意圖_ 。 It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. 播放器狀態尚未進入「正在播放」，而是「正在開始」。[必要的工作階段參數](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) ，必須包含在請 `params` 求主體的地圖中。  在後端，這個呼叫會產生 Adobe Analytics 起始呼叫。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### 動作2 - Ping計時器開始 {#Action-2}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式開始 Ping 事件計時器 | 0 | 0 |  |

**實作詳細資訊**

啟動ping計時器。 如果有前段廣告，則先ping事件應觸發1秒，否則觸發10秒。

### 動作3 —— 廣告插播開始 {#Action-3}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告插播開始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

廣告追蹤只能在廣告插播中進行。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### 動作4 —— 廣告開始 {#Action-4}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #1 開始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

開始追蹤第一個前段廣告，其持續時間為 15 秒。包括該 `adStart` 的中繼資料。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### 動作5 - Ad ping {#Action-5}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每1秒Ping一次後端。 （後續的和ping不是為了簡短而顯示的。）

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作6 —— 廣告完成 {#Action-6}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #1 完成 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤第一個前段廣告的結尾。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 動作7 —— 廣告開始 {#Action-7}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #2 開始 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤第二個前段廣告開始，其持續時間為 7 秒。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 操作8 - Ad ping {#Action-8}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每1秒Ping一次後端。 （後續的和ping不是為了簡短而顯示的。）

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作9 —— 廣告完成 {#Action-9}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #2 完成 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤第二個前段廣告的結尾。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 動作10 —— 廣告插播完成 {#Action-10}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告插播完成 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

廣告插播結束。在整個廣告插播期間，播放狀態均保持「正在播放」。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### 動作11 —— 播放內容 {#Action-11}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤播放事件 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

在 `adBreakComplete` 事件之後，使用 `play` 事件將播放器置於「正在播放」狀態。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### 動作12 —— 章節開始 {#Action-12}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤章節開始事件 | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

在播放事件後，追蹤第一個章節的開始。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### 動作13 - Ping {#Action-13}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每隔 10 秒 Ping 後端一次

**範例要求內文**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作14 —— 緩衝區開始 {#Action-14}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 發生緩衝開始事件 | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤移至「緩衝」狀態。

**範例要求內文**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### 動作15 —— 緩衝區結束（播放） {#Action-15}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 緩衝結束後，應用程式追蹤內容的繼續播放 | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

緩衝在 3 秒後結束，因此請讓播放器回復「正在播放」狀態。您必須傳送另一個追蹤播放事件來結束緩衝狀態。**在`play`呼叫`bufferStart`後，會向後端輸入"bufferEnd"呼叫，** 因此不需要事 `bufferEnd` 件。

**範例要求內文**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### 動作16 - Ping {#Action-16}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每隔 10 秒 Ping 後端一次

**範例要求內文**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 行動17 —— 章節結束 {#Action-17}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式追蹤章節結束 | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

第一個章節結束，緊接著是第二個廣告插播。

**範例要求內文**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### 動作18 —— 廣告插播開始 {#Action-18}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告插播開始 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

持續 8 秒的中段廣告: 傳送 `adBreakStart`。

**範例要求內文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### 動作19 —— 廣告開始 {#Action-19}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告 #3 開始 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤中段廣告。

**範例要求內文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 操作20 —— 廣告Ping {#Action-20}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每1秒Ping一次後端。 （後續的和ping不是為了簡短而顯示的。）

**範例要求內文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作21 —— 廣告完成 {#Action-21}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告 #1 完成 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

中段廣告完成。

**範例要求內文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 動作22 —— 廣告插播完成 {#Action-22}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告插播完成 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

廣告插播完成。

**範例要求內文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### 行動23 —— 章節開始 {#Action-23}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤第 2 章開始 | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**



**範例要求內文**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### 動作24 - Ping {#Action-24}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每隔 10 秒 Ping 後端一次

**範例要求內文**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作25 —— 暫停 {#Action-25}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 使用者按下「暫停」 | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

使用者動作會將播放狀態移至「已暫停」。

**範例要求內文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### 動作26 - Ping {#Action-26}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每隔 10 秒 Ping 後端一次播放器依然處於「正在緩衝」狀態；使用者在內容中停滯 20 秒。怒氣沖沖...

**範例要求內文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作27 —— 播放內容 {#Action-27}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 使用者按下「播放」繼續播放主要內容 | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

將播放狀態改變為「正在播放」。**`play`之後的`pauseStart`呼叫意味著傳送「」呼叫到後端**，因此不需要 `resume`resume 事件。

**範例要求內文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### 動作28 - Ping {#Action-28}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

每隔 10 秒 Ping 後端一次

**範例要求內文**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 行動29 —— 章結束 {#Action-29}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 第 2 章結束 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

追蹤第二個和最終章節的結尾。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### 操作30 —— 會話完成 {#Action-30}

| Action | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 使用者完成觀賞內容到結束為止。 | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**實作詳細資訊**

傳送 `sessionComplete` 到後端，指出使用者已完成所有內容的觀賞。

**範例要求內文**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**沒有尋找事件？ -** 媒體收集 API 對於 `seekStart` 或 `seekComplete` 事件的支援並不明確。這是因為有些播放器會在使用者拖曳時產生大量的此類事件，因此只要數百位使用者就能輕易讓後端服務的網路頻寬遇到瓶頸。Adobe 根據裝置時間戳記來運算心率持續時間，而非依賴播放點位置，藉此解決搜尋事件明確支援的問題。

