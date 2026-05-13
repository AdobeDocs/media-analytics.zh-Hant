---
title: 實作與報告
description: 了解如何實作播放器狀態追蹤功能，包括
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# 實作與報告

在播放工作階段期間，每個狀態發生 (從開始到結束) 都必須個別追蹤。 Media SDK和Media Collection API提供此功能的追蹤方法。

Media SDK包含兩種自訂狀態追蹤方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API包含兩個以`media.stateName`作為必要引數的事件：

`stateStart` 與 `stateEnd`

## Media SDK 實作

播放器狀態開始

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

播放器狀態結束

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Media Collection API 實作

播放器狀態開始

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

播放器狀態結束

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## 狀態量度

針對每個個別狀態提供的量度在經過計算後會推送至 Adobe Analytics，作為「內容資料」參數，並儲存以供產生報告。 每個狀態有三種可用的量度：

* `a.media.states.[state.name].set = true` — 如果每個特定資料流播放至少設定一次狀態，則此量度設為 true。
* `a.media.states.[state.name].count = 4` — 識別每個個別資料流播放期間的狀態發生次數
* `a.media.states.[state.name].time = 240` — 識別每個個別資料流播放的總狀態持續時間 (秒)

## 報告

在播放器狀態追蹤啟用報表套裝後，所有的播放器狀態量度，均可用來產生任何可在 Analysis Workspace 中使用的視覺化報表或元件 (區段、計算量度)。 您可以使用「媒體報表設定」（「編輯設定>媒體管理>媒體報表」），從Admin Console為每個個別報表啟用這些量度。

![](assets/report-setup.png)

在Analysis Workspace中，所有新屬性都位於「量度」面板中。 例如，您可以依 `full screen` 搜尋，在量度面板中檢視全螢幕資料。

![](assets/full-screen-report.png)

## 將播放器狀態量度匯入至 Adobe Experience Platform

儲存在 Analytics 中的資料可用於任何用途，而您可以使用 XDM 將播放器狀態量度匯入至 Adobe Experience Platform，並與 Customer Journey Analytics 搭配使用。 標準狀態屬性具有特定屬性，自訂狀態則是可用自訂事件使用的屬性。
