---
title: 在 iOS 上追蹤廣告
description: 使用 Media SDK 在 iOS 應用程式中實作廣告追蹤。
uuid: e979e679-cde5-4c30-8f34-867feceac13a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 iOS 上追蹤廣告{#track-ads-on-ios}

>[!IMPORTANT]
>
>下列指示提供使用 2.x SDK 實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK。](/help/sdk-implement/download-sdks.md)

## 廣告追蹤常數

| 常數名稱 | 說明   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | 用於追蹤廣告插播開始事件的常數 |
| `ADBMediaHeartbeatEventAdBreakComplete` | 用於追蹤廣告插播事件的常數 |
| `ADBMediaHeartbeatEventAdStart` | 用於追蹤廣告開始事件的常數 |
| `ADBMediaHeartbeatEventAdComplete` | 用於追蹤廣告完成事件的常數 |
| `ADBMediaHeartbeatEventAdSkip` | 用於追蹤廣告略過事件的常數 |

## 實施步驟

1. 識別廣告插播界限何時開始 (包括前段)，並使用廣告插播資訊建立 `AdBreakObject`。

   `AdBreakObject` 參考資料:

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告插播名稱，例如前段、中段和後段。 | 是 |
   | `position` | 內容中廣告插播的編號位置從 1 開始。 | 是 |
   | `startTime` | 廣告插播開始時的播放點值。 | 是 |

   廣告插播物件建立:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. 在 `MediaHeartbeat` 例項中使用 `AdBreakStart` 呼叫 `trackEvent()` 以開始追蹤廣告插播。

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. 識別廣告何時開始，並使用廣告資訊建立 `AdObject` 例項。

   `AdObject` 參考資料:

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 廣告的易記名稱。 | 是 |
   | `adId` | 廣告的唯一識別碼。 | 是 |
   | `position` | 廣告插播中的廣告編號位置從 1 開始。 | 是 |
   | `length` | 廣告長度 | 是 |

   廣告物件建立:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到媒體追蹤工作階段。

   * [在 iOS 上實作標準廣告中繼資料](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告的資料:

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. 在 `MediaHeartbeat` 例項中使用 `AdStart` 事件呼叫 `trackEvent()` 以開始追蹤廣告播放。

   將參考加入您的自訂中繼資料變數 (或空白物件)，作為事件呼叫中的第三個參數:

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. 當廣告播放達到廣告結尾時，請使用 `AdComplete` 事件呼叫 `trackEvent()`。

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件.

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件進行追蹤:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

如需詳細資訊，請參閱追蹤案例[具有前段廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)。
