---
title: 實作事件要求
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 實作事件要求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

在使用[工作階段要求取得工作階段 ID 後，請使用[事件要求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)來進行所有後續追蹤呼叫。](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)請在要求的 JSON 內文中指定播放點位置和時間戳記、事件類型，以及任何想加入的選用參數。

[事件要求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)的 JSON 要求內文，其結構與「工作階段」要求相同。即便如此，還是請參閱 [JSON 驗證結構](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)來瞭解參數需求和類型。
