---
title: 說明追蹤體驗品質
description: 使用 Media SDK 追蹤體驗品質 (QoE、QoS) 的相關概觀。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 99%

---

# 概觀{#overview}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

體驗品質追蹤包含服務品質 (QoS) 和錯誤追蹤，此兩項皆為選用元素，且&#x200B;**不是**&#x200B;核心媒體追蹤實作的必要元素。 您可以使用媒體播放器 API 識別 QoS 相關的變數以及錯誤追蹤。 以下為追蹤體驗品質的重要元素：

## 播放器事件 {#player-events}

### 對於任何 QoS 量度變更：

建立或更新播放適用的 QoS 物件例項。 [QoS API 參考資料](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 所有位元速率變更事件

呼叫 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 實作QOS

1. 識別媒體播放中何時有任何 QoS 量度變更，並利用 QoS 資訊建立 `MediaObject`，以及更新新的 QoS 資訊。

   QoSObject 變數：

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
   >更新 QoS 物件，並在每次位元速率變更時呼叫位元速率變更事件。 如此可提供最精確的 QoS 資料。

以下程式碼範例將 JavaScript 2.x SDK 用於 HTML5 媒體播放器。 您應該將此程式碼與核心媒體播放程式碼一起使用。

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
