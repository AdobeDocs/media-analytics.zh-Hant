---
title: 了解如何在 Chromecast 上追蹤體驗品質
description: 「了解如何在 Chromecast 上使用 Media SDK 實作體驗品質 (QoE、QoS) 追蹤。」
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '294'
ht-degree: 100%

---

# 在 Chromecast 上追蹤體驗品質{#track-quality-of-experience-on-chromecast}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 概觀 {#overview}

體驗品質追蹤包含服務品質 (QoS) 和錯誤追蹤，此兩項皆為選用元素，且&#x200B;**不是**&#x200B;核心媒體追蹤實作的必要元素。您可以使用媒體播放器 API 識別 QoS 相關的變數以及錯誤追蹤。

## 播放器事件 {#player-events}

### 所有位元速率變更事件

* 建立/更新播放適用的 QoS 物件例項，`qosObject`
* 呼叫 `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### 播放器錯誤

呼叫 `trackError("media error id");`

## 實作 {#implement}

1. 識別媒體播放期間位元速率是否變更，並且利用 QoS 資訊建立 `MediaObject` 例項。

   **QoSObject 變數：**

   >[!TIP]
   >
   >唯有在您計劃追蹤 QoS 時，才須使用這些變數。

   | 變數 | 說明 | 必填 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   **QoS 物件建立：** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >更新 QoS 物件，並在每次位元速率變更時呼叫位元速率變更事件。如此可提供最精確的 QoS 資料。

1. 請確定 `getQoSObject()` 方法會傳回最新的 QoS 資訊。
1. 當媒體播放器發生錯誤，且播放器 API 可使用錯誤事件時，請利用 `trackError()` 來擷取錯誤資訊(請參閱[概觀](/help/use-cases/track-errors/track-errors-overview.md))。

   >[!TIP]
   >
   >追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError()` 之後呼叫 `trackSessionEnd()`，以確定媒體追蹤工作階段已關閉。
