---
seo-title: 在 iOS 上追蹤緩衝
title: 在 iOS 上追蹤緩衝
uuid: 4f4db23a-489b-4b41-bb6 e-393ec64 d52 a2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 上追蹤緩衝{#track-buffering-on-ios}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 緩衝追蹤常數


| 常數名稱 | 說明     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | 用於追蹤緩衝開始事件的常數 |
| `ADBMediaHeartbeatEventBufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實施緩衝

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
