---
title: 追蹤體驗品質說明
description: 使用 Media SDK 追蹤體驗品質 (QoE、QoS) 的相關概述。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 98%

---

# 概觀{#overview}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

體驗品質追蹤包含服務品質 (QoS) 和錯誤追蹤，此兩項皆為選用元素，且&#x200B;**不是**&#x200B;核心媒體追蹤實施的必要元素。您可以使用媒體播放器 API 識別 QoS 相關的變數以及錯誤追蹤。以下為追蹤體驗品質的重要元素:

## 播放器事件 {#player-events}

### 對於任何 QoS 量度變更:

建立或更新播放適用的 QoS 物件例項。[QoS API 參考資料](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 所有位元速率變更事件

呼叫 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 實作 QoS

1. 識別媒體播放中何時有任何 QoS 量度變更，並利用 QoS 資訊建立 `MediaObject`，以及更新新的 QoS 資訊。

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

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件。

   >[!IMPORTANT]
   >
   >更新 QoS 物件，並在每次位元速率變更時呼叫位元速率變更事件。如此可提供最精確的 QoS 資料。

以下程式碼範例將 JavaScript 2.x SDK 用於 HTML5 媒體播放器。您應該將此程式碼與核心媒體播放程式碼一起使用。

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
