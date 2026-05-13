---
title: 了解如何在 Roku 上追蹤錯誤
description: 了解如何在 Roku 上使用 Media SDK 實作錯誤追蹤。
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/S18A1AAxOQYLn216PtfA3IyO6F9j-WAAeHzlQn5UKvI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 100%

---

# 在 Roku 上追蹤錯誤{#track-errors-on-roku}

下列指示提供所有 2.x SDK 之間實作的指引。

>[!IMPORTANT]
>
> 若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南：[下載 SDK](/help/getting-started/download-sdks.md)。

## 實作錯誤追蹤

1. 追蹤媒體播放器錯誤：

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤將不會停止媒體追蹤工作階段。 如果媒體播放器錯誤使得播放無法繼續，請透過在呼叫 `trackError` 之後呼叫 `trackSessionEnd`，以確定媒體追蹤工作階段已關閉。
