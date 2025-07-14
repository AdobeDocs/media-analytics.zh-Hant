---
title: 傳送 Ping 事件
description: Ping事件是串流媒體集合的心率。 了解如何針對主要內容或廣告追蹤傳送計時 Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 51%

---

# 傳送 Ping 事件{#sending-ping-events}

**您必須從播放開始10秒後，每隔10秒引發一次Ping事件，不論其他已傳送的API事件為何。 這同時適用於主要內容和廣告追蹤。**

Ping事件是串流媒體收集的「心率」。 Ping 呼叫唯一需要的參數是 `eventType: ping`，另外需要搭配 `playerTime` 物件 (播放點位置和時間戳記)。

以下程式碼片段示範如何針對主要內容實作計時 Ping 機制 (10 秒間隔)：

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
