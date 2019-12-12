---
title: 在 JavaScript 上追蹤搜尋
description: 本主題說明如何在瀏覽器應用程式 (JS) 中使用 Media SDK 實作搜尋追蹤。
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 上追蹤搜尋{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 搜尋追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `SeekStart` | 用於追蹤搜尋開始事件的常數。 |
| `SeekComplete` | 用於追蹤搜尋完成事件的常數。 |

## 實作搜尋

1. 從媒體播放器上聽取播放搜尋事件，並在搜尋開始事件通知上使用 `SeekStart` 事件追蹤搜尋:

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. 在來自媒體播放器的搜尋完成通知上，使用 `SeekComplete` 事件來追蹤搜尋的結尾:

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

如需詳細資訊，請參閱追蹤案例[主要內容中具有搜尋的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
