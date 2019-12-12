---
title: 在 JavaScript 上追蹤體驗品質
description: 本主題說明如何在瀏覽器應用程式 (JS) 中使用 Media SDK 實作體驗品質 (QoE、QoS) 追蹤。
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 上追蹤體驗品質{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 實作 QoS

1. 識別媒體播放期間位元速率是否變更，並且利用 QoS 資訊建立 `MediaObject` 例項。

   QoSObject 變數:

   >[!TIP]
   >
   >唯有在您計劃追蹤 QoS 時，才須使用這些變數。

   | 變數 | 說明 | 必填 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   QoS 物件建立:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件:

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >更新 QoS 物件，並在每次位元速率變更時呼叫位元速率變更事件。如此可提供最精確的 QoS 資料。

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. 當媒體播放器發生錯誤，且播放器 API 可使用錯誤事件時，請利用 `trackError()` 來擷取錯誤資訊(請參閱[概述](/help/sdk-implement/track-errors/track-errors-overview.md))。

   >[!TIP]
   >
   >追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError()` 之後呼叫 `trackSessionEnd()`，以確定媒體追蹤工作階段已關閉。

