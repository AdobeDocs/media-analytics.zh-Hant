---
seo-title: 在 iOS 上追蹤體驗品質
title: 在 iOS 上追蹤體驗品質
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 上追蹤體驗品質{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 實施QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject 變數:

   | 變數 | 說明 | 必要 |
   | --- | --- | :---: |
   | `bitrate` | 目前位元速率 | 是 |
   | `startupTime` | 啟動時間 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 掉格的數量 | 是 |

   >[!TIP]
   >
   >只有在您計畫追蹤QoS時，才需要這些變數。

   QoS 物件建立:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. 請確定 `getQoSObject` 方法會傳回最新的 QoS 資訊。
1. 當播放轉換位元速率時，呼叫媒體心率例項中的 `BitrateChange` 事件:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >更新QoS物件，並在每次位元速率變更時呼叫位元速率變更事件。 如此可提供最精確的 QoS 資料。

