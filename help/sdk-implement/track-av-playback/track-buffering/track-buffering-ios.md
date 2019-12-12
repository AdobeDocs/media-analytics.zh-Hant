---
title: 在 iOS 上追蹤緩衝
description: 說明如何在 iOS 上追蹤緩衝事件。
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 iOS 上追蹤緩衝{#track-buffering-on-ios}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 緩衝追蹤常數


| 常數名稱 | 說明 |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | 用於追蹤緩衝開始事件的常數 |
| `ADBMediaHeartbeatEventBufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實作緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
