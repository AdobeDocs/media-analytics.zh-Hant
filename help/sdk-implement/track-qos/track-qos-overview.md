---
seo-title: 概述
title: 概述
uuid: 4d73c47f-d0 a4-4228-9040-d6432311 c9 eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 概述{#overview}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. 您可以使用媒體播放器API來識別與QoS和錯誤追蹤相關的變數。以下為追蹤體驗品質的重要元素:

## 播放器事件 {#player-events}

### 對於任何 QoS 量度變更:

建立或更新播放適用的 QoS 物件例項。[QoS API參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 所有位元速率變更事件

呼叫 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 實施者QoS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

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

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件。

   >[!IMPORTANT]
   >
   >更新QoS物件，並呼叫每個位元速率變更上的位元速率變更事件。如此可提供最精確的 QoS 資料。

下列範例程式碼使用HTML媒體播放器的JavaScript2.x SDK。您應使用此程式碼搭配核心媒體播放程式碼。

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

