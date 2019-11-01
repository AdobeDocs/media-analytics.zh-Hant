---
title: 在 Chromecast 上追蹤體驗品質
description: 本主題說明使用Chromecast上的Media SDK來實作體驗品質(QoE、QoS)追蹤。
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 上追蹤體驗品質{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 概述 {#overview}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. 您可以使用媒體播放器API來識別與QoS和錯誤追蹤相關的變數。

## 播放器事件 {#player-events}

### 所有位元速率變更事件

* 建立/更新播放適用的 QoS 物件例項，`qosObject`
* 呼叫 `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### 播放器錯誤

呼叫 `trackError(“media error id”);`

## 實作 {#implement}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **QoSObject 變數:**

   >[!TIP]
   >
   >只有在您計畫追蹤QoS時，才需要這些變數。

   | 變數 | 說明 | 必要 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   **QoS 物件建立:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >更新QoS物件，並在每次位元速率變更時呼叫位元速率變更事件。 如此可提供最精確的 QoS 資料。

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

