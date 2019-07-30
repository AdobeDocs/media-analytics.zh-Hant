---
seo-title: 在工作階段回應緩慢時，將事件加入佇列
title: 在工作階段回應緩慢時，將事件加入佇列
uuid: 39ea59d9-89d3-4087-a806-48a43 ef0 c98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在工作階段回應緩慢時，將事件加入佇列{#queueing-events-when-sessions-response-is-slow}

媒體收集 API 為 RESTful API，這表示您可以發出 HTTP 要求並等候回應。This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. 這很重要，因為所有後續追蹤呼叫都需要使用工作階段ID。

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

>[!NOTE]
>
>[事件要求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)除了 HTTP 回應代碼外，不會將資料傳回用戶端。

請查閱發佈中的參考播放器，取得在接受工作階段 ID 之前處理事件的方法。例如:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**處理任何已加入佇列的事件 -** 參考播放器會依照下列方法處理已加入佇列的事件:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

繼續處理後續發生的追蹤事件。
