---
title: 說明追蹤錯誤
description: 使用 Media SDK 深入了解錯誤追蹤。
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
exl-id: 61c5f835-d66c-4621-a0af-2e4f47a922ac
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/YCA19QFHZ3AiWa3hJfz7QD52pTxOxPW2iFoWfGfTz8s
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 96
ht-degree: 100%

---

# 概觀{#overview}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤。

   在錯誤事件上，呼叫帶有錯誤資訊的 `trackError`。

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。 如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
