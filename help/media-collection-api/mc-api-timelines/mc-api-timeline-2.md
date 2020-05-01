---
title: 時間軸 2 - 使用者放棄工作階段
description: null
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
translation-type: tm+mt
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8

---


# 時間軸 2 - 使用者放棄工作階段 {#timeline--2-user-abandons-session}

## VOD、前段廣告、中段廣告、使用者提早放棄內容

下列圖表說明播放點時間軸和使用者動作的對應時間軸。以下呈現每個動作的詳細資料及其隨附要求。


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## 動作詳細資料

### 動作 1 - 開始工作階段 {#Action-1}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 按下「自動播放」或「播放」按鈕 | 0 | 0 | `/api/v1/sessions` |

**實作詳細資料**

這個呼叫代表&#x200B;_使用者有意願播放_&#x200B;影片。它會傳回工作階段 ID (`{sid}`)，給予用來識別工作階段中所有後續追蹤呼叫的用戶端。播放器狀態尚未進入「正在播放」，而是「正在開始」。要求內容的 `params` 對映必須包含[強制工作階段參數](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。在後端，這個呼叫會產生 Adobe Analytics 起始呼叫。

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
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### 動作 2 - 啟動 Ping 計時器 {#Action-2}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式啟動 Ping 事件計時器 | 0 | 0 |  |

**實作詳細資料**

啟動應用程式的 Ping 計時器。如果有前段廣告，第一個 Ping 事件則應在 1 秒引發；如果沒有，則為 10 秒。

### 動作 3 - 廣告插播開始 {#Action-3}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告插播開始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

必須追蹤前段廣告。廣告追蹤只能在廣告插播中進行。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### 動作 4 - 廣告開始 {#Action-4}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #1 開始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

12 秒的廣告開始。

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
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### 動作 5 - 廣告 Ping {#Action-5}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

每隔 1 秒 Ping 後端一次。(為了簡單起見，將不會顯示後續廣告 Ping。)

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

### 動作 6 - 廣告完成 {#Action-6}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告 #1 完成 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

第一個前段廣告結束。

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

### 動作 7 - 廣告插播完成 {#Action-7}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤前段廣告插播完成 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

廣告插播結束。整個廣告插播期間，播放器一直保持「正在播放」狀態。

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

### 動作 8 - 播放內容 {#Action-8}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤播放事件 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

將播放器改變為「正在播放」狀態；開始追蹤內容播放的開始。

**範例要求內文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### 動作 9 - Ping {#Action-9}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

每隔 10 秒 Ping 後端一次。

**範例要求內文**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作 10 - Ping {#Action-10}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

每隔 10 秒 Ping 後端一次。

**範例要求內文**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作 11 - 錯誤 {#Action-11}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 發生錯誤，應用程式傳送錯誤資訊。 | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**


**範例要求內文**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### 動作 12 - 播放內容 {#Action-12}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式從錯誤中復原，使用者按下「播放」 | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**



**範例要求內文**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### 動作 13 - Ping {#Action-13}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 應用程式傳送 Ping 事件 | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

每隔 10 秒 Ping 後端一次。

**範例要求內文**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 動作 14 - 廣告插播開始 {#Action-14}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告插播開始 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

持續 8 秒的中段廣告：傳送 `adBreakStart`。

**範例要求內文**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### 動作 15 - 廣告開始 {#Action-15}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 追蹤中段廣告 #1 開始 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

追蹤中段廣告。

**範例要求內文**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### 動作 16 - 關閉應用程式 {#Action-16}

| 動作 | 動作時間軸 (秒) | 播放點位置 (秒) | 用戶端要求 |
| --- | :---: | :---: | --- |
| 使用者關閉應用程式。應用程式判斷使用者已放棄觀看，且不會回到此工作階段。 | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**實作詳細資料**

傳送 `sessionEnd` 給 VA 後端，指出應立即關閉工作階段，而且不需要進一步處理。

**範例要求內文**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```
