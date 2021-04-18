---
title: 在播放器中設定 HTTP 要求類型
description: 在播放器中設定 HTTP 要求類型
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 100%

---

# 設定 HTTP 要求類型 {#setting-the-http-request-type}

所有媒體收集 API 要求的要求內文都必須採用 JSON 格式，因此您應該要在播放器中設定內容要求類型。以 JavaScript 為例，您可以依照以下範例設定 `Content-Type` 要求標題:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
