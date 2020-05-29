---
title: 使用JavaScript 2.x追蹤錯誤
description: 本主題說明如何在瀏覽器應用程式 (JS) 中使用 Media SDK 實作錯誤追蹤。
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 89%

---


# 使用JavaScript 2.x追蹤錯誤{#track-errors-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤:

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
