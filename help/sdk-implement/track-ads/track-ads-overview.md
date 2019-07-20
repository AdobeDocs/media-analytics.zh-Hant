---
seo-title: 概述
title: 概述
uuid: 1607798b-c6 ef-4d60-8e40-e958 c345 c09 c
translation-type: tm+mt
source-git-commit: 56e8716ea37049b95a59a82144bbad0e882c16b4

---


# 概述{#overview}

>[!IMPORTANT]
>
>下列指示提供使用2.x SDK進行實施的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK.](../../sdk-implement/download-sdks.md)

廣告播放包含追蹤廣告插播、廣告開始、廣告完成，以及廣告略過。使用媒體播放器的API來識別關鍵播放器事件，並填入必要和選擇性的廣告變數。See the comprehensive list of metadata here: [Ad parameters.](../../metrics-and-metadata/ad-parameters.md)

## Player events {#player-events}


### 在廣告插播開始時

>[!NOTE]
>包括前置卷

* 為廣告插播建立 `adBreak` 物件例項，例如, `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### 在每個廣告資產開始時

* 為廣告資產建立廣告物件例項，例如, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* 呼叫廣告開始的 `trackEvent`。

### 在每個廣告完成時

* 呼叫廣告完成的 `trackEvent`。

### 在廣告略過時

* 呼叫廣告略過的 `trackEvent`。

### 在廣告插播完成時

* 呼叫廣告插播完成的 `trackEvent`。

## Implement ad tracking {#section_83E0F9406A7743E3B57405D4CDA66F68}

### 廣告追蹤常數

| 常數名稱 | 說明   |
|---|---|
| `AdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `AdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `AdStart` | 用於追蹤廣告開始事件的常數 |
| `AdComplete` | 用於追蹤廣告完成事件的常數 |
| `AdSkip` | 用於追蹤廣告略過事件的常數 |

### 實施步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   `AdBreakObject` 參考：

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告插播名稱，例如前段、中段和後段。 | 是 |
   | `position` | 內容中廣告插播的編號位置從 1 開始。 | 是 |
   | `startTime` | 廣告插播開始時的播放點值。 | 是 |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. 識別廣告何時開始，並使用廣告資訊建立 `AdObject` 例項。

   `AdObject` 參考：

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告的易記名稱。 | 是 |
   | `adId` | 廣告的唯一識別碼。 | 是 |
   | `position` | 廣告插播中的廣告編號位置從 1 開始。 | 是 |
   | `length` | 廣告長度 | 是 |

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到追蹤工作階段。

   * **標準廣告中繼資料 -** 對於標準廣告中繼資料，請使用平台的索引鍵，建立標準廣告中繼資料索引鍵值配對的字典。
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告的資料。

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數。

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件.
1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件加以追蹤.

>[!IMPORTANT]
>
>Make sure you do NOT increment the content player playhead (`l:event:playhead`) during ad playback (`s:asset:type=ad`). 如果您執行，「內容逗留時間」度量會受到負面影響。

下列範例程式碼使用HTML媒體播放器的JavaScript2.x SDK。

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```

## 驗證 {#section_5F1783F5FE2644F1B94B0101F73D57EB}

### 廣告開始

開始播放個別廣告時，會依下列順序傳送三個索引鍵呼叫:

1. 視訊廣告分析開始
1. 心率廣告開始
1. 心率分析開始

呼叫 1 和 2 包含自訂和標準的其他中繼資料變數。

### 廣告播放

在廣告播放過程中，心率廣告播放呼叫每一秒便會傳送到心率伺服器。

### 廣告完成

在廣告的 100% 點上，將傳送心率廣告完成呼叫。

### 廣告略過

略過廣告時，不會傳送任何事件，因此追蹤呼叫不會包含廣告資訊。

>[!TIP]
>
>不會在廣告中斷開始和廣告中斷完成時傳送唯一呼叫。

