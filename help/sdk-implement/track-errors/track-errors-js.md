---
seo-title: 在 JavaScript 上追蹤錯誤
title: 在 JavaScript 上追蹤錯誤
uuid: 5fc5fc-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 JavaScript 上追蹤錯誤{#track-errors-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 實施錯誤追蹤

1. 追蹤媒體播放器錯誤：

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

