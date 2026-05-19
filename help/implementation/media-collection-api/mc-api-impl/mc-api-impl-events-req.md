---
title: 實作事件要求
description: 了解如何在取得工作階段 ID 後使用事件要求端點進行所有後續的追蹤呼叫
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
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
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# 實作事件要求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

使用[工作階段要求](../mc-api-ref/mc-api-sessions-req.md)取得工作階段識別碼之後，請將[事件要求](../mc-api-ref/mc-api-events-req.md)用於所有後續的追蹤呼叫。 請在要求的JSON內文中指定播放點位置和時間戳記、事件型別，以及任何想加入的選用引數。

[事件要求](../mc-api-ref/mc-api-events-req.md)的 JSON 要求內文，其結構與「工作階段」要求相同。即便如此，還是請參閱 [JSON 驗證結構](../mc-api-ref/mc-api-json-validation.md)來瞭解參數需求和類型。
