---
title: 在 Chromecast 上追蹤緩衝
description: 說明在Chromecast上追蹤緩衝事件。
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 上追蹤緩衝{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 緩衝追蹤常數


| 常數名稱 | 說明     |
|---|---|
| `BufferStart` | 用於追蹤緩衝開始事件的常數 |
| `BufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實現緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
