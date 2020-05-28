---
title: 使用JavaScript 3.x追蹤體驗品質
description: 本主題說明在使用JavaScript 3x的瀏覽器應用程式中使用Media SDK實作體驗品質(QoE、QoS)追蹤。
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# 使用JavaScript 3.x追蹤體驗品質{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 3.x SDK 之間實作的指引。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 實施QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   QoEObject變數：

   >[!TIP]
   >
   >唯有在您計劃追蹤 QoS 時，才須使用這些變數。

   | 變數 | 類型 | 說明 |
   | --- | --- | --- |
   | `bitrate` | 數字 | 目前位元速率 |
   | `startupTime` | 數字 | 啟動時間 |
   | `fps` | 數字 | FPS 值 |
   | `droppedFrames` | 數字 | 掉格的數量 |

   QoE對象建立：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   ```

1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >更新QoE物件，並在每次位元速率變更時呼叫位元速率變更事件。 這樣可提供最精確的QoE資料。

1. 請務必呼叫方 `updateQoEObject()` 法，為SDK提供最新的QoE資訊。
1. 當媒體播放器發生錯誤，且播放器 API 可使用錯誤事件時，請利用 `trackError()` 來擷取錯誤資訊(請參閱[概述](/help/sdk-implement/track-errors/track-errors-overview.md))。

   >[!TIP]
   >
   >追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError()` 之後呼叫 `trackSessionEnd()`，以確定媒體追蹤工作階段已關閉。
