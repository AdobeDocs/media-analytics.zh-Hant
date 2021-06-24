---
title: 了解如何使用JavaScript 3.x追蹤搜尋
description: 了解如何使用瀏覽器應用程式(JS 3.x)中的Media SDK來追蹤搜尋開始和搜尋完成事件。
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 62%

---

# 使用JavaScript 3.x追蹤搜尋{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 3.x SDK 之間實作的指引。若您正在實作任何舊版SDK，您可以在此處下載開發人員指南：[下載SDK。](/help/sdk-implement/download-sdks.md)

## 搜尋追蹤常數

| 常數名稱 | 說明 |
|---|---|
| `SeekStart` | 用於追蹤搜尋開始事件的常數。 |
| `SeekComplete` | 用於追蹤搜尋完成事件的常數。 |

## 實作搜尋

1. 從媒體播放器上聽取播放搜尋事件，並在搜尋開始事件通知上使用 `SeekStart` 事件追蹤搜尋:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. 在來自媒體播放器的搜尋完成通知上，使用 `SeekComplete` 事件來追蹤搜尋的結尾:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

如需詳細資訊，請參閱追蹤案例[主要內容中具有搜尋的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
