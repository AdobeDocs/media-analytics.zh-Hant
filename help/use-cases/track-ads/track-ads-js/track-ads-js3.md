---
title: 了解如何使用JavaScript 3.x追蹤廣告
description: 使用 Media SDK 在瀏覽器 (JS) 應用程式中實作廣告追蹤。
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 80%

---

# 使用JavaScript 3.x追蹤廣告{#track-ads-on-javascript}

下列指示提供使用 3.x SDK 實作的指引。

>[!IMPORTANT]
>
>若您正在實作任何舊版SDK，您可以在此處下載開發人員指南： [下載SDK。](/help/getting-started/download-sdks.md)

## 廣告追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `AdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `AdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `AdStart` | 用於追蹤廣告開始事件的常數 |
| `AdComplete` | 用於追蹤廣告完成事件的常數 |
| `AdSkip` | 用於追蹤廣告略過事件的常數 |

## 實施步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   `AdBreakObject` 參考資料:

   | 變數名稱 | 類型 | 說明 |
   | --- | --- | --- |
   | `name` | 字串 | 表示廣告插播名稱（前段、中段和後段）的非空白字串。 |
   | `position` | 數字 | 廣告插播的編號位置從 1 開始。 |
   | `startTime` | 數字 | 廣告插播開始時的播放點值。 |

   廣告插播物件建立:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. 在 `MediaHeartbeat` 例項中使用 `AdBreakStart` 呼叫 `trackEvent()` 以開始追蹤廣告插播。

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. 識別廣告何時開始，並使用廣告資訊建立 `AdObject` 例項。

   `AdObject` 參考資料:

   | 變數名稱 | 類型 | 說明 |
   | --- | --- | --- |
   | `name` | 字串 | 表示廣告名稱的非空字串。 |
   | `adId` | 字串 | 表示廣告識別碼的非空字串。 |
   | `position` | 數字 | 廣告在廣告插播內的數量位置，從1開始。 |
   | `length` | 數字 | 表示廣告長度的正數。 |

   廣告物件建立:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到媒體追蹤工作階段。

   * [在 JavaScript 上實作標準廣告中繼資料](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告的資料:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. 在 `MediaHeartbeat` 例項中使用 `AdStart` 事件呼叫 `trackEvent()` 以開始追蹤廣告播放。

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. 當廣告播放達到廣告結尾時，請使用 `AdComplete` 事件呼叫 `trackEvent()`:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件進行追蹤:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

如需詳細資訊，請參閱追蹤案例[具有前段廣告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。
