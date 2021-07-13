---
title: 了解如何在Roku上追蹤廣告
description: 使用 Media SDK 在 Roku 應用程式中實作廣告追蹤。
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 97%

---

# 在 Roku 上追蹤廣告{#track-ads-on-roku}

>[!IMPORTANT]
>
>下列指示提供使用 2.x SDK 實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK。](/help/sdk-implement/download-sdks.md)

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

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 廣告插播名稱，例如前段、中段和後段。 | 是 |
   | `position` | 廣告插播的編號位置從 1 開始。 | 是 |
   | `startTime` | 廣告插播開始時的播放點值。 | 是 |

   ```
   ‘ Create an adbreak info object 
   adBreakInfo = adb_media_init_adbreakinfo() 
   adBreakInfo.name = <ADBREAK_NAME> 
   adBreakInfo.startTime = <START_TIME> 
   adBreakInfo.position = <POSITION>
   ```

1. 在 `MediaHeartbeat` 例項中使用 `AdBreakStart` 呼叫 `trackEvent()` 以開始追蹤廣告插播。

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. 識別廣告資產何時開始，並使用廣告資訊建立 `AdObject` 例項。

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration) 
   ```

1. 可選擇透過內容資料變數，將標準和/或廣告中繼資料附加到媒體追蹤工作階段。

   * [在 Roku 上實作標準廣告中繼資料](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **自訂廣告中繼資料 -** 對於自訂中繼資料，請建立自訂資料變數的變數物件，並填入目前廣告資產的資料:

      ```
      contextData = {} 
      contextData["adinfo1"] = "adinfo2" 
      contextData["adinfo2"] = "adinfo2"
      ```

1. 在 `MediaHeartbeat` 例項中使用 `AdStart` 事件呼叫 `trackEvent()` 以開始追蹤廣告播放:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. 當廣告資產播放達到廣告結尾時，請使用 `AdComplete` 事件呼叫 `trackEvent()`。

   ```
   standardAdMetadata = {} 
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. 如果由於使用者選擇略過廣告而導致廣告播放未完成，請追蹤 `AdSkip` 事件:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. 如果在相同 `AdBreak` 內有任何其他廣告，請再次重複步驟 3 到 7。
1. 當廣告插播完成時，請使用 `AdBreakComplete` 事件進行追蹤:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

如需詳細資訊，請參閱追蹤案例[具有前段廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)。
