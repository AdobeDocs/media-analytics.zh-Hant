---
title: 實作事件要求
description: 實作事件要求
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 100%

---

# 實作事件要求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

使用[事件要求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)進行所有後續的追蹤呼叫；請先使用以下操作取得工作階段 ID：[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)請在要求的 JSON 內文中指定播放點位置和時間戳記、事件類型，以及任何想加入的選用參數。

[事件要求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)的 JSON 要求內文，其結構與「工作階段」要求相同。即便如此，還是請參閱 [JSON 驗證結構](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)來瞭解參數需求和類型。
