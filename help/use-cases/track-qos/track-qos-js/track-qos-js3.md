---
title: 了解如何使用 JavaScript 3.x 追蹤體驗品質
description: 「了解如何在使用 JavaScript 3x 的瀏覽器應用程式中使用 Media SDK 實作體驗品質 (QoE、QoS) 追蹤。」
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 99%

---

# 使用 JavaScript 3.x 追蹤體驗品質{#track-quality-of-experience-on-javascript}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作任何舊版的 SDK，您可以在此處下載開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 實作QOE

1. 識別媒體播放期間位元速率是否變更，並且利用 QoE 資訊建立 `qoeObject` 例項。

   QoEObject 變數：

   >[!TIP]
   >
   >唯有在您計劃追蹤 QoS 時，才須使用這些變數。

   | 變數 | 類型 | 說明 |
   | --- | --- | --- |
   | `bitrate` | 數字 | 目前位元速率 |
   | `startupTime` | 數字 | 啟動時間 |
   | `fps` | 數字 | FPS 值 |
   | `droppedFrames` | 數字 | 掉格的數量 |

   QoE 物件建立：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件：

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
   >更新 QoE 物件，並在每次位元速率變更時呼叫位元速率變更事件。如此可提供最精確的 QoE 資料。

1. 請務必呼叫 `updateQoEObject()` 方法以向 SDK 提供最新的 QoE 資訊。
1. 當媒體播放器發生錯誤，且播放器 API 可使用錯誤事件時，請利用 `trackError()` 來擷取錯誤資訊(請參閱[概觀](/help/use-cases/track-errors/track-errors-overview.md))。

   >[!TIP]
   >
   >追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError()` 之後呼叫 `trackSessionEnd()`，以確定媒體追蹤工作階段已關閉。
