---
title: 了解如何在Roku上追蹤錯誤
description: 了解如何在Roku上使用Media SDK實作錯誤追蹤。
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 81%

---

# 在 Roku 上追蹤錯誤{#track-errors-on-roku}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
> 若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
