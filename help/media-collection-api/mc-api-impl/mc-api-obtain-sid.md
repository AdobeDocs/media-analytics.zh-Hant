---
seo-title: 取得工作階段 ID
title: 取得工作階段 ID
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 取得工作階段 ID{#obtaining-a-session-id}

This code snippet from the Reference Player shows one way of coding a [Sessions request,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) along with extracting the Session ID (and the Media Collection API version) from the Location header in the response:

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

