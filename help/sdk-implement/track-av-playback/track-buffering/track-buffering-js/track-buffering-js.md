---
title: 使用JavaScript 2.x追蹤緩衝
description: 說明如何在瀏覽器應用程式 (JS) 中追蹤緩衝事件。
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 91%

---


# 使用JavaScript 2.x追蹤緩衝{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 緩衝追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `BufferStart` | 用於追蹤緩衝開始事件的常數 |
| `BufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實作緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝。

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾。

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。