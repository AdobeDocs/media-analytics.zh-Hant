---
title: 在 Chromecast 上追蹤廣告
description: 使用 Media SDK 在 Chromecast 應用程式中實作廣告追蹤。
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 上追蹤廣告{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>下列指示提供使用 2.x SDK 實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK。](/help/sdk-implement/download-sdks.md)

## 廣告追蹤常數

| 常數名稱 | 說明   |
|---|---|
| `AdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `AdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `AdStart` | 用於追蹤廣告開始事件的常數 |
| `AdComplete` | 用於追蹤廣告完成事件的常數 |
| `AdSkip` | 用於追蹤廣告略過事件的常數 |

## 實施步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   廣告插播物件建立:[ createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. 在 `MediaHeartbeat` 例項中使用 `AdBreakStart` 呼叫 `trackEvent()` 以開始追蹤廣告插播: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. 識別廣告資產何時開始，並使用廣告資訊建立 `AdObject` 例項。

   廣告物件建立:[ createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到媒體追蹤工作階段。

   * **標準廣告中繼資料 -** 針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告資產的資料:

1. 使用 `AdStart` 事件呼叫 `trackEvent()` 以開始追蹤廣告播放。

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. 當廣告資產播放達到廣告結尾時，請使用 `AdComplete` 事件呼叫 `trackEvent()`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 6。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件進行追蹤: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

如需詳細資訊，請參閱追蹤案例[具有前段廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)。
