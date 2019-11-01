---
title: 概述
description: 使用Media SDK進行錯誤追蹤。
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 概述{#overview}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 實施錯誤追蹤

1. 追蹤媒體播放器錯誤。

   在錯誤事件上，呼叫帶有錯誤資訊的 `trackError`。

>[!NOTE]
>
>追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

