---
title: 實施與報告
description: 本主題說明如何實作播放器狀態追蹤功能，包括。
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 實施與報告

在播放作業階段期間，必須個別追蹤每個狀態發生（從開始到結束）。 Media SDK和Media Collection API提供此功能的新追蹤方法。

Media SDK包含兩種新的自訂狀態追蹤方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API包含兩個以&quot;media.stateName&quot;為必要參數的新事件：

`stateStart` 與 `stateEnd`

## Media SDK實作

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


## Media Collection API實作

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

針對每個個別狀態提供的量度會計算並推送至Adobe Analytics作為「內容資料」參數，並儲存以供報告之用。 每個狀態有三個可用的度量：

* `a.media.states.(media.state.name).set = true` — 如果每個流的特定播放至少將狀態設定一次，則設為true。
* `a.media.states.(media.state.name).count = 4` — 識別每次個別播放串流期間發生狀態的次數
* `a.media.states.(media.state.name).time = 240` — 識別每個串流個別播放的總狀態持續時間（秒）

## 報表

所有狀態度量都可用於任何報表視覺化或元件（區段、計算度量）。
TBD —— 檢查源／維基以瞭解更新資訊——從AW拍攝螢幕

## 將播放器指定的量度匯入Adobe Experience Platform

儲存在Analytics中的資料可用於任何用途，而播放器狀態量度可使用XDM匯入至Adobe Experience Platform，並與客戶歷程分析搭配使用。 標準狀態屬性具有特定屬性，而自訂狀態是屬性可透過自訂事件使用。 如需詳細資訊，請參閱XDM身分的屬性清單，網址為「連結至量度清單」。
