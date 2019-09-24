---
seo-title: 在播放器中設定 HTTP 要求類型
title: 在播放器中設定 HTTP 要求類型
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# 設定HTTP請求類型 {#setting-the-http-request-type}

所有媒體收集 API 要求的要求內文都必須採用 JSON 格式，因此您應該要在播放器中設定內容要求類型。以 JavaScript 為例，您可以依照以下範例設定 `Content-Type` 要求標題:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

