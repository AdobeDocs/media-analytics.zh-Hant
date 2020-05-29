---
title: 實施與報告
description: 本主題說明如何實作播放器狀態追蹤功能，包括。
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# 實施與報告

在播放作業階段期間，必須個別追蹤每個狀態發生（從開始到結束）。 Media SDK和Media Collection API提供此功能的新追蹤方法。

Media SDK包含兩種新的自訂狀態追蹤方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API包含兩個新事件，其中 `media.stateName` 為必要參數：

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

* `a.media.states.[state.name].set = true` — 如果每個流的特定播放至少將狀態設定一次，則設為true。
* `a.media.states.[state.name].count = 4` — 識別每次個別播放串流期間發生狀態的次數
* `a.media.states.[state.name].time = 240` — 識別每個串流個別播放的總狀態持續時間（秒）

## 報表

在報表套裝啟用播放器狀態追蹤後，所有播放器狀態度量都可用於分析工作區或元件（區段、計算量度）中的任何報表視覺化。 新量度可從「管理控制台」使用「媒體報表設定」（編輯設定>媒體管理>媒體報表），針對每個個別報表啟用。

![](assets/report-setup.png)

在Analytics工作區中，所有新屬性都位於量度面板中。 例如，您可以依據搜尋， `full screen` 在量度面板中檢視全螢幕資料。

![](assets/full-screen-report.png)

## 將播放器指定的量度匯入Adobe Experience Platform

儲存在Analytics中的資料可用於任何用途，而播放器狀態量度可使用XDM匯入至Adobe Experience Platform，並與客戶歷程分析搭配使用。 標準狀態屬性具有特定屬性，而自訂狀態是屬性可透過自訂事件使用。
