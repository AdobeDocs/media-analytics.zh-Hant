---
title: 取得工作階段 ID
description: null
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 取得工作階段 ID{#obtaining-a-session-id}

這段來自參考播放器的程式碼片段示範如何編寫[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)的程式碼，以及示範如何從回應中的 Location 標題擷取工作階段 ID (和媒體收集 API 版本)。

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```

