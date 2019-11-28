---
title: 從 1.x 轉換為 2.x API
description: 本主題包含 API 參考資料的連結，並列出 Media SDK 1.x 版和 2.x 版的必要和選用追蹤 API。
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 從 API 1.x 轉換至 2.x  {#one-x-to-two-x-conv}

## Media SDK 2.x API 參考資料

* [Android API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Chromecast API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## 必要追蹤* API:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | 不適用 |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject、mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | 不適用 |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

所有選用的追蹤 API (例如「廣告」、「章節」、「位元速率變更」、「搜尋」和「緩衝」) 現已成為單一 `trackEvent` API 的一部分。[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) API 接收代表您有意追蹤的事件類型的常數參數:

## 選用的 trackEvent API:

| VHL 1.x | VHL 2.x |
|---|---|
| 在 `AdBreakInfo` () 中傳回有效的 `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| 在 `VideoPlayerPlugin.getAdBreakInfo()` () 中傳回 null。 | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| 在 `VideoPlayerPlugin.getAdInfo()` () 中傳回 null。 | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| 在 `VideoPlayerPlugin.getChapterInfo()` () 中傳回 null。 | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

