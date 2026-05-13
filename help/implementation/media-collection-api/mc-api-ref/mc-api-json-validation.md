---
title: 串流媒體服務JSON驗證結構
description: 什麼是 Steaming Media JSON 驗證結構，如何使用它們判斷每種事件類型的正確要求內文參數。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ZWKv1LJKc8qLkZYpcNdDFEs8Er70toRCoufarMcgVKQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 71%

---

# JSON 驗證結構{#json-validation-schemas}

串流媒體收集後端會使用JSON驗證結構來驗證每種事件型別的要求引數。 您可以使用這些結構，將它們當做目前 MA API 使用之參數類型的可信來源。

`GET https://{uri}/api/v1/schemas/{event-type}`

如需使用 JSON 驗證結構的詳細資訊，請參閱[驗證事件要求](../mc-api-impl/mc-api-validate-reqs.md)。
