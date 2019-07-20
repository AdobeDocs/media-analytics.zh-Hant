---
seo-title: 在 Android 上追蹤廣告
title: 在 Android 上追蹤廣告
uuid: 4a4249fb-dc39-4947-a14 d-a51 d972 f32 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 Android 上追蹤廣告{#track-ads-on-android}

>[!IMPORTANT]
>
>下列指示提供使用2.x SDK進行實施的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK.](../../sdk-implement/download-sdks.md)

## 廣告追蹤常數

| 常數名稱 | 說明 |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `MediaHeartbeat.Event.AdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `MediaHeartbeat.Event.AdStart` | 用於追蹤廣告開始事件的常數 |
| `MediaHeartbeat.Event.AdComplete` | 用於追蹤廣告完成事件的常數 |
| `MediaHeartbeat.Event.AdSkip` | 用於追蹤廣告略過事件的常數 |

## 實施步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   `AdBreakObject` 參考：

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告插播名稱，例如前段、中段和後段。 | 是 |
   | `position` | 內容中廣告插播的編號位置從 1 開始。 | 是 |
   | `startTime` | 廣告插播開始時的播放點值。 | 是 |

   廣告插播物件建立:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
   ```

1. 識別廣告何時開始，並使用廣告資訊建立 `AdObject` 例項。

   `AdObject` 參考：

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告的易記名稱。 | 是 |
   | `adId` | 廣告的唯一識別碼。 | 是 |
   | `position` | 廣告插播中的廣告編號位置從 1 開始。 | 是 |
   | `length` | 廣告長度 | 是 |

   廣告物件建立:

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. (選擇性)透過上下文資料變數，將標準和/或廣告中繼資料附加至媒體追蹤工作階段。

   * [在 Android 上實作標準廣告中繼資料](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告的資料:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件進行追蹤:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

如需詳細資訊，請參閱追蹤案例[具有前段廣告的 VOD 播放](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md)。
