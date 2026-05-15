---
title: 說明追蹤廣告
description: 有關如何使用 Media SDK 實作廣告追蹤的概觀。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 77%

---

# 概觀{#overview}

下列指示提供使用 2.x SDK 實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK。](/help/getting-started/download-sdks.md)

廣告播放包含追蹤廣告插播、廣告開始、廣告完成，以及廣告略過。 請使用媒體播放器的 API 來識別重要的播放器事件，並填入必要和選用的廣告變數。

## 播放器事件 {#player-events}

### 在廣告插播開始時

>[!NOTE]
>包括前段廣告

* 為廣告插播建立 `adBreak` 物件例項， 例如，`adBreakObject`。

* 使用 `trackEvent` 呼叫廣告插播開始的 `adBreakObject`。

### 在每個廣告資產開始時

* 為廣告資產建立廣告物件例項， 例如，`adObject`。
* 填入廣告中繼資料 `adCustomMetadata`。
* 呼叫廣告開始的 `trackEvent`。

### 在每個廣告完成時

* 呼叫廣告完成的 `trackEvent`。

### 在廣告略過時

* 呼叫廣告略過的 `trackEvent`。

### 在廣告插播完成時

* 呼叫廣告插播完成的 `trackEvent`。

## 實作廣告追蹤 {#implement-ad-tracking}

### 廣告追蹤常數

| 常數名稱 | 說明   |
|---|---|
| `AdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `AdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `AdStart` | 用於追蹤廣告開始事件的常數 |
| `AdComplete` | 用於追蹤廣告完成事件的常數 |
| `AdSkip` | 用於追蹤廣告略過事件的常數 |

### 實作步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   `AdBreakObject` 參考資料：

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 廣告插播名稱，例如，前段、中段和後段。 | 是 |
   | `position` | 內容中廣告插播的編號位置從1開始。 | 是 |
   | `startTime` | 廣告插播開始時的播放點值。 | 是 |

1. 在 `MediaHeartbeat` 例項中使用 `AdBreakStart` 呼叫 `trackEvent()` 以開始追蹤廣告插播。

1. 識別廣告何時開始，並使用廣告資訊建立 `AdObject` 例項。

   `AdObject` 參考資料：

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 廣告的易記名稱。 | 是 |
   | `adId` | 廣告的唯一識別碼。 | 是 |
   | `position` | 廣告插播中的廣告編號位置從1開始。 | 是 |
   | `length` | 廣告長度 | 是 |

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到追蹤工作階段。

   * **標準廣告中繼資料 —**&#x200B;針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典。
   * **自訂廣告中繼資料 —**&#x200B;對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告的資料。

1. 在 `MediaHeartbeat` 例項中使用 `AdStart` 事件呼叫 `trackEvent()` 以開始追蹤廣告播放。

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數。

1. 當廣告播放達到廣告結尾時，請使用 `AdComplete` 事件呼叫 `trackEvent()`。

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件.
1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件加以追蹤.

>[!IMPORTANT]
>
>請勿在廣告播放期間 (`s:asset:type=ad`) 增加內容播放器播放點 (`l:event:playhead`)。 若這麼做，會對「內容逗留時間」量度產生不利的影響。

以下程式碼範例將 JavaScript 2.x SDK 用於 HTML5 媒體播放器。

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

>[!MORELIKETHIS]
>
>* [廣告插播開始](/help/implementation/events/ads/ad-break-start.md)
>* [廣告開始](/help/implementation/events/ads/ad-start.md)
>* [廣告完成](/help/implementation/events/ads/ad-complete.md)
>* [廣告略過](/help/implementation/events/ads/ad-skip.md)
>* [廣告插播完成](/help/implementation/events/ads/ad-break-complete.md)
