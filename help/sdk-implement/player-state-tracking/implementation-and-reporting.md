---
title: 實作與報告
description: 此主題說明如何實作播放器狀態追蹤功能，包括
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 58%

---


# 實作與報告

在播放工作階段期間，每個狀態發生 (從開始到結束) 都必須個別追蹤。Media SDK 和 Media Collection API 為此功能提供新的追蹤方法。

Media SDK 提供兩種新的自訂狀態追蹤方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


The Media Collection API includes two new events that have `media.stateName` as the required parameter:

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

## 報表

在報表套裝啟用播放器狀態追蹤後，所有播放器狀態度量都可用於分析工作區或元件（區段、計算量度）中的任何報表視覺化。 新量度可從「管理控制台」使用「媒體報表設定」（編輯設定>媒體管理>媒體報表），針對每個個別報表啟用。

![](assets/report-setup.png)

在Analytics工作區中，所有新屬性都位於量度面板中。 例如，您可以依據搜尋， `full screen` 在量度面板中檢視全螢幕資料。

![](assets/full-screen-report.png)

## 將播放器狀態量度匯入至 Adobe Experience Platform

儲存在 Analytics 中的資料可用於任何用途，而您可以使用 XDM 將播放器狀態量度匯入至 Adobe Experience Platform，並與 Customer Journey Analytics 搭配使用。標準狀態屬性具有特定屬性，而自訂狀態是屬性，則可使用自訂事件。 有關標準狀態屬性的其他資訊，請參 *閱「播放器狀態參數」頁面上的「XDM身份的屬性清單*[](/help/metrics-and-metadata/player-state-parameters.md) 」部分。
