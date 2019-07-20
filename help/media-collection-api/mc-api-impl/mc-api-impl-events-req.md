---
seo-title: 實作事件要求
title: 實作事件要求
uuid: 3bfa313c-ff74-4e2 e-bbde-6f4 a6221 d85 b
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 實作事件要求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) 在請求的JSON內文中指定播放磁頭位置和時間戳記、事件類型以及您想要包含的任何選用參數。

[事件請求的JSON請求主體](../../media-collection-api/mc-api-ref/mc-api-events-req.md) 具有與「工作階段」請求相同的結構，但檢查 [JSON驗證架構](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) 的參數需求和類型。
