---
title: 了解如何在 Android 上追蹤緩衝
description: 了解如何在 Android 上追蹤緩衝事件。
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# 在 Android 上追蹤緩衝{#track-buffering-on-android}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 緩衝追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | 用於追蹤緩衝開始事件的常數 |
| `MediaHeartbeat.Event.BufferComplete` | 用於追蹤緩衝完成事件的常數 |

## 實作緩衝

1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝：

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null);
   }
   ```

1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾：

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null);
   }
   ```

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/use-cases/tracking-scenarios/vod-buffering.md)。
