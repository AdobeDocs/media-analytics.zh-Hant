---
seo-title: 在 Roku 上追蹤緩衝
title: 在 Roku 上追蹤緩衝
uuid: 6666b270-9aa3-42ff-95a8-f12502022 d47
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# 在 Roku 上追蹤緩衝{#track-buffering-on-roku}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## 緩衝追蹤常數

| 常數名稱 | 說明     |
|---|---|
| `BufferStart` | 用於追蹤緩衝開始事件的常數 |
| `BufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實施緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝。

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾。

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](../../../sdk-implement/tracking-scenarios/vod-buffering.md)。
