---
title: 解決主要內容出現在廣告之間的問題
description: 瞭解如何處理廣告之間的意外main：play呼叫。
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 76%

---


# 處理出現在廣告之間的間隙{#resolving-main-play-appearing-between-ads}

## 問題

在某些追蹤情況下，您可能會遭遇 `main:play` 呼叫意外出現在某個廣告的結尾與下一個廣告的開始之間的情況。如果廣告完成呼叫與下一個廣告開始呼叫之間的延遲超過 250 毫秒，Media SDK 便會回復到傳送 `main:play` 呼叫。如果這個回復到 `main:play` 的動作發生在前段廣告插播期間，內容開始量度的設定可能會過早。

上述廣告之間的間隙會由Media SDK解譯為主要內容，因為這些間隙不會與任何廣告內容重疊。 Media SDK上未設定任何廣告資訊，且播放器處於播放狀態。 如果沒有廣告資訊，且播放器狀態正在播放，則Media SDK依預設會將與主要內容的間隔時間計入在內。 它不能將播放持續期間視為空的廣告資訊。

## IDENTIFICATION

在使用 Adobe Debug 或 Charles 之類的封包 Sniffer 時，如果您在前段廣告插播期間發現以下順序的心率呼叫：

* 工作階段開始：`s:event:type=start` &amp; `s:asset:type=main`
* 廣告開始：`s:event:type=start` &amp; `s:asset:type=ad`
* 廣告播放：`s:event:type=play` &amp; `s:asset:type=ad`
* 廣告完成：`s:event:type=complete` &amp; `s:asset:type=ad`
* 主要內容播放：`s:event:type=play` &amp; `s:asset:type=main` **(未預期)**

* 廣告開始：`s:event:type=start` &amp; `s:asset:type=ad`
* 廣告播放：`s:event:type=play` &amp; `s:asset:type=ad`
* 廣告完成：`s:event:type=complete` &amp; `s:asset:type=ad`
* 主要內容播放：`s:event:type=play` &amp; `s:asset:type=main` **(預期)**

## 解析度

***延遲觸發廣告完成呼叫。***

延遲呼叫第一個廣告的 `trackEvent:AdComplete`，緊接著呼叫第二個廣告的 `trackEvent:AdStart`，藉此從播放器內部處理間隙。第一個廣告完成時，應用程式應延遲呼叫 `AdComplete` 事件。請務必呼叫廣告插播中最後一個廣告的 `trackEvent:AdComplete`。如果播放器能識別目前的廣告資產是廣告插播中的最後一個廣告，請立即呼叫 `trackEvent:AdComplete`。此解析度將導致少於1秒的額外廣告時間歸因到先前的廣告單位。

**在廣告插播 (包括前段廣告) 開始時：**

* 為廣告插播建立 `adBreak` 物件例項，如 `adBreakObject`。

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**在每個廣告資產開始時：**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >唯有在上一個廣告未完成時才進行呼叫。請考慮使用布林值來維持上一個廣告的 &quot;`isinAd`&quot; 狀態。

* 為廣告資產建立物件例項，如 `adObject`。
* 填入廣告中繼資料 `adCustomMetadata`。
* 呼叫 `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* 如果這是前段廣告插播中的第一個廣告，請呼叫 `trackPlay()`。

**在每個廣告資產完成時：**

* **請勿進行呼叫**

  >[!NOTE]
  >
  >如果應用程式知道這是廣告插播中的最後一個廣告，請在這裡呼叫 `trackEvent:AdComplete`，並略過 `trackEvent:AdBreakComplete` 中 `trackEvent:AdComplete` 的設定。

**略過廣告時：**

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**廣告插播完成時：**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >如果您已在前述最後一個 `trackEvent:AdComplete` 呼叫時執行本步驟，可以予以忽略。

* 呼叫 `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
