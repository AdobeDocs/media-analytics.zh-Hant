---
title: 了解如何使用 JavaScript 2.x 追蹤搜尋
description: 了解如何在瀏覽器應用程式 (JS 2.x) 中使用 Media SDK 來追蹤搜尋開始和搜尋完成事件。
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/wQkUvm0BhqYGd9q-k2YKe2f0kkhjkM3hpwDYuAIw3QU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 100%

---

# 使用 JavaScript 2.x 追蹤搜尋{#track-seeking-on-javascript}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 搜尋追蹤常數

| 常數名稱 | 說明     |
|---|---|
| `SeekStart` | 用於追蹤搜尋開始事件的常數。 |
| `SeekComplete` | 用於追蹤搜尋完成事件的常數。 |

## 實作搜尋

1. 從媒體播放器上聽取播放搜尋事件，並在搜尋開始事件通知上使用 `SeekStart` 事件追蹤搜尋：

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. 在來自媒體播放器的搜尋完成通知上，使用 `SeekComplete` 事件來追蹤搜尋的結尾：

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

如需詳細資訊，請參閱追蹤案例[主要內容中具有搜尋的 VOD 播放](/help/use-cases/tracking-scenarios/vod-seeking.md)。
