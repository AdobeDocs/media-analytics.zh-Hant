---
title: JSON 驗證結構
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# JSON 驗證結構{#json-validation-schemas}

Media Analytics 後端會使用 JSON 驗證結構來驗證每種事件類型的要求參數。您可以使用這些結構，將它們當做目前 MA API 使用之參數類型的可信來源。

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

如需使用 JSON 驗證結構的詳細資訊，請參閱[驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)。
