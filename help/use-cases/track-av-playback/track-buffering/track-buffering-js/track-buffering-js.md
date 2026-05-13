---
title: 了解如何使用 JavaScript 2.x 追蹤緩衝
description: 了解如何在瀏覽器應用程式 (JS) 中追蹤緩衝事件。
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/uw6vM-TESRbHRcMy2hIVQYNm3GJFIaUZTTOkOHeMih4
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 126
ht-degree: 100%

---

# 使用 JavaScript 2.x 追蹤緩衝{#track-buffering-on-javascript}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 緩衝追蹤常數

| 常數名稱 | 說明     |
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

如需詳細資訊，請參閱追蹤案例[具有緩衝的 VOD 播放](/help/use-cases/tracking-scenarios/vod-buffering.md)。
