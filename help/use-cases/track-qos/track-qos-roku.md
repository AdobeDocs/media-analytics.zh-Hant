---
title: 了解如何在 Roku 上追蹤體驗品質
description: 瞭解如何在Roku上使用Media SDK實作體驗品質(QoE、QoS)追蹤。
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
exl-id: cd84c26d-ad91-4179-9532-83408030ff3e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-e2JKBn8IB9Kk-MEVIlQq6IY5Wuevlp6GrpkM96xuX4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 200
ht-degree: 91%

---

# 在 Roku 上追蹤體驗品質{#track-quality-of-experience-on-roku}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 實作QOS

1. 識別媒體播放期間位元速率是否變更，並且利用 `mediaUpdateQoS` API 更新 Media SDK 上的 QoS 資訊。

   QoSObject 變數：

   >[!TIP]
   >
   >只有在追蹤 QoS 時，才須使用這些變數。

   | 變數 | 說明 | 必填 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   例如：

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:

    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. 當播放轉換位元速率時，請呼叫 `trackEvent(BitrateChange)`，通知 Media SDK 位元速率已變更。

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >您必須使用更新的位元速率值來呼叫 `updateQoSObject`。

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```

    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. 當媒體播放器發生錯誤，且播放器 API 可使用錯誤事件時，請利用 `trackError()` 來擷取錯誤資訊 (請參閱[概觀](/help/use-cases/track-errors/track-errors-overview.md))。

   >[!TIP]
   >
   >追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。 如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError()` 之後呼叫 `trackSessionEnd()`，以確定媒體追蹤工作階段已關閉。
