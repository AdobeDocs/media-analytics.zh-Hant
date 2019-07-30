---
seo-title: 在 Roku 上追蹤體驗品質
title: 在 Roku 上追蹤體驗品質
uuid: a8b242ab-da3 c-4297-1eef-f0 b9684 ef56 a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Roku 上追蹤體驗品質{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 實施者QoS

1. Identify when the bitrate changes during media playback, and use the `mediaUpdateQoS` API to update the QoS info on the Media SDK.

   QoSObject 變數:

   >[!TIP]
   >
   >只有在您追蹤QoS時才需要這些變數。

   | 變數 | 說明 | 必要 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   例如:

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

1. When playback switches bitrates, call `trackEvent(BitrateChange)` to notify the Media SDK that the Bitrate changed.

   ```
   ADBMobile().trackMediaEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >You need to call `updateQoSObject` with the updated bitrate value.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

