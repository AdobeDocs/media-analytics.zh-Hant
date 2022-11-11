---
title: 串流Media Analytics JSON驗證結構
description: 什麼是串流媒體JSON驗證結構，以及如何使用這些結構來判斷每種事件類型的正確要求內文參數。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 63%

---

# JSON 驗證結構{#json-validation-schemas}

Media Analytics 後端會使用 JSON 驗證結構來驗證每種事件類型的要求參數。您可以使用這些結構，將它們當做目前 MA API 使用之參數類型的可信來源。

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

如需使用 JSON 驗證結構的詳細資訊，請參閱[驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)。
