---
title: 在工作階段回應緩慢時將事件加入佇列
description: 了解當播放器觸發事件後傳回工作階段ID時，該做什麼。
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 92%

---

# 在工作階段回應緩慢時，將事件加入佇列{#queueing-events-when-sessions-response-is-slow}

媒體收集 API 為 RESTful API，這表示您可以發出 HTTP 要求並等候回應。唯有當您在開始播放視訊時發出[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)來取得工作階段 ID 時，才需要注意這項重點。這很重要，因為所有後續追蹤呼叫都需要此工作階段 ID。

您的播放器可能會&#x200B;_在工作階段回應從後端返回之前_ (連同工作階段 ID 參數) 引發事件。如果發生這種情形，應用程式必須將所有在[工作階段要求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)與其回應之間抵達的追蹤事件加入佇列。當「工作階段」回應抵達時，您應該先處理所有已加入佇列的[事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)，接著才能開始以 [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) 呼叫處理&#x200B;_即時_&#x200B;事件。

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
