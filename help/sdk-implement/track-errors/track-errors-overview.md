---
title: 概述
description: 使用 Media SDK 進行錯誤追蹤。
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 概述{#overview}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤。

   在錯誤事件上，呼叫帶有錯誤資訊的 `trackError`。

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。

