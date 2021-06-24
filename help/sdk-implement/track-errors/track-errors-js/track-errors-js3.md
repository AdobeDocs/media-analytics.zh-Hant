---
title: 了解如何使用JavaScript 3.x追蹤錯誤
description: 了解如何在瀏覽器應用程式(JS)中使用Media SDK實作錯誤追蹤。
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 54%

---

# 使用JavaScript 3.x追蹤錯誤{#track-errors-on-javascript}

>[!IMPORTANT]
>
>下列指示提供所有 3.x SDK 之間實作的指引。若您正在實作任何舊版SDK，您可以在此處下載開發人員指南：[下載SDK。](/help/sdk-implement/download-sdks.md)

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
