---
title: 傳送 Ping 事件
description: Ping事件是串流Media Analytics的心率。 了解如何針對主要內容或廣告追蹤傳送計時Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 78%

---

# 傳送 Ping 事件{#sending-ping-events}

**針對主要內容，您必須從播放開始 10 秒後，每隔 10 秒引發一次 Ping 事件，不論其他已傳送的 API 事件為何。針對廣告追蹤，您必須每隔 1 秒引發一次 Ping 事件。**

就字面上來說，Ping 事件是 Media Analytics 的「心率」。Ping 呼叫唯一需要的參數是 `eventType: ping`，另外需要搭配 `playerTime` 物件 (播放點位置和時間戳記)。

以下程式碼片段示範如何針對主要內容實作計時 Ping 機制 (10 秒間隔):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
