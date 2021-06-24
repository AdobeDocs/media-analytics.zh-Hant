---
title: 了解如何在iOS上追蹤錯誤
description: 了解如何在iOS上使用Media SDK實作錯誤追蹤。
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
exl-id: c4ce7092-a102-41da-80a6-a4359f925708
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 81%

---

# 在 iOS 上追蹤錯誤{#track-errors-on-ios}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤:

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
