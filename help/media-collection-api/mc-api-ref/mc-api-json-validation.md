---
title: JSON 驗證結構
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# JSON 驗證結構{#json-validation-schemas}

Media Analytics後端會使用JSON驗證結構描述來驗證每個事件類型的請求參數。 這些結構可用於MA API中的參數類型，並作為當前權限。

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
