---
title: 了解如何使用JavaScript 3.x追蹤緩衝
description: 了解如何在瀏覽器應用程式(JS)中追蹤緩衝事件。
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 65%

---

# 使用JavaScript 3.x追蹤緩衝{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 3.x SDK 之間實作的指引。若您正在實作任何舊版SDK，您可以在此處下載開發人員指南：[下載SDK。](/help/sdk-implement/download-sdks.md)

## 緩衝追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `BufferStart` | 用於追蹤緩衝開始事件的常數 |
| `BufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實作緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝。

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾。

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
