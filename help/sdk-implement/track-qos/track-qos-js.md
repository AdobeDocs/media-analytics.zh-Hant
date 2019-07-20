---
seo-title: 在 JavaScript 上追蹤體驗品質
title: 在 JavaScript 上追蹤體驗品質
uuid: 3bc762a2-9706-4b62-aua91-747f461 dd13 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 JavaScript 上追蹤體驗品質{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## 實施者QoS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject 變數:

   >[!TIP]
   >
   >只有當您打算追蹤QoS時才需要這些變數。

   | 變數 | 說明 | 必要 |
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
   >更新QoS物件，並呼叫每個位元速率變更上的位元速率變更事件。如此可提供最精確的 QoS 資料。

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

