---
seo-title: 解決廣告間出現的主重頭戲
title: 解決廣告間出現的主重頭戲
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# 解決 main:play 出現在廣告之間的問題{#resolving-main-play-appearing-between-ads}

## 問題

在某些追蹤情況下，您可能會遭遇 `main:play` 呼叫意外出現在某個廣告的結尾與下一個廣告的開始之間的情況。If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. 如果這個回復到 `main:play` 的動作發生在前段廣告插播期間，內容開始量度的設定可能會過早。

Media SDK 會將前述廣告間的間隙解讀為主要內容，因為它與任何廣告內容並無重疊之處。Media SDK 沒有任何已設定的廣告資訊，而且播放器正處於播放狀態。如果沒有廣告資訊，而且播放器處於播放狀態，Media SDK 預設會將間隙的持續時間視為主要內容。它不能將播放持續期間視為空的廣告資訊。

## IDENTIFICATION

在使用Adobe Debug或網路封包嗅探器（例如Charles）時，如果您在前段廣告插播期間依此順序看到下列心率呼叫：

* 工作階段開始: `s:event:type=start` &amp; `s:asset:type=main`
* 廣告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 廣告播放: `s:event:type=play` &amp; `s:asset:type=ad`
* 廣告完成: `s:event:type=complete` &amp; `s:asset:type=ad`
* 主要內容播放： `s:event:type=play` &amp; `s:asset:type=main`**（非預期）**

* 廣告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 廣告播放: `s:event:type=play` &amp; `s:asset:type=ad`
* 廣告完成: `s:event:type=complete` &amp; `s:asset:type=ad`
* 主要內容播放： `s:event:type=play` 與 `s:asset:type=main`**（預期）**

## 解析度

***延遲觸發廣告完成呼叫。***

延遲呼叫第一個廣告的 `trackEvent:AdComplete`，緊接著呼叫第二個廣告的 `trackEvent:AdStart`，藉此從播放器內部處理間隙。第一個廣告完成時，應用程式應延遲呼叫 `AdComplete` 事件。請務必呼叫廣告插播中最後一個廣告的 `trackEvent:AdComplete`。如果播放器能識別目前的廣告資產是廣告插播中的最後一個廣告，請立即呼叫 `trackEvent:AdComplete`。這個解決方案將能使少於 1 秒的廣告額外逗留時間歸因於先前廣告單元。

**在廣告插播 (包括前段廣告) 開始時:**

* 為廣告插播建立 `adBreak` 物件例項，如 `adBreakObject`。

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**在每個廣告資產開始時:**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >只有在上一個廣告未完成時才呼叫此功能。 請考慮使用布林值來維持上一個廣告的 "`isinAd`" 狀態。

* 為廣告資產建立物件例項，如 `adObject`。
* Populate the ad metadata, `adCustomMetadata`.
* 呼叫 `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**在每個廣告資產完成時:**

* **不要打電話**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**略過廣告時:**

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**廣告插播完成時:**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

