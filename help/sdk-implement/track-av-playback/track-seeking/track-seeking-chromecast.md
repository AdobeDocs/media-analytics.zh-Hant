---
seo-title: 在 Chromecast 上追蹤搜尋
title: 在 Chromecast 上追蹤搜尋
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Chromecast 上追蹤搜尋{#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 搜尋追蹤常數

| 常數名稱 | 說明     |
|---|---|
| `SeekStart` | 用於追蹤搜尋開始事件的常數。 |
| `SeekComplete` | 用於追蹤搜尋完成事件的常數。 |

## 實作搜尋

1. 從媒體播放器上聽取播放搜尋事件，並在搜尋開始事件通知上使用 `SeekStart` 事件追蹤搜尋: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   ```

1. 在來自媒體播放器的搜尋完成通知上，使用 `SeekComplete` 事件來追蹤搜尋的結尾: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   ```

如需詳細資訊，請參閱追蹤案例[主要內容中具有搜尋的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
