---
title: 傳送 Ping 事件
description: Ping事件是Adobe串流媒體服務的心率。 了解如何針對主要內容或廣告追蹤傳送計時 Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6R7DILB56bcHgAki-Lvto3yYbuhf-wYfklvPElDeM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 110
ht-degree: 50%

---

# 傳送 Ping 事件{#sending-ping-events}

**您必須從播放開始10秒後，每隔10秒引發一次Ping事件，不論其他已傳送的API事件為何。 這同時適用於主要內容和廣告追蹤。**

Ping事件是Adobe串流媒體服務的「心率」。 Ping 呼叫唯一需要的參數是 `eventType: ping`，另外需要搭配 `playerTime` 物件 (播放點位置和時間戳記)。

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
