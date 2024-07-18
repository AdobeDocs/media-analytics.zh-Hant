---
title: SDK 除錯
description: 了解媒體 SDK 提供的追蹤/記錄。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%

---

# SDK 除錯{#sdk-debugging}

您可以啟用和停用記錄功能。Media SDK 提供可在整個媒體追蹤堆疊中使用的追蹤/記錄擴充功能機制。您可以在「設定」物件上設定 `debugLogging` 標幟，藉此啟用或停用記錄功能。

## 除錯記錄的程式碼範例

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT (Chromecast、Roku)

ADBMobile 程式庫能透過 `setDebugLogging` 方法提供除錯記錄。所有生產應用程式的除錯記錄都應設定為 `false`。

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## 記錄訊息

記錄訊息會遵循此格式：

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp**：這是目前的 CPU 時間 (GMT 時區)
* **level**：定義的訊息層次有 4 個：
   * INFO - 通常是來自應用程式的輸入資料 (驗證播放器名稱、視訊 ID 等)
   * DEBUG - 除錯記錄檔，開發人員用來除錯更複雜的問題
   * WARN - 指出可能的整合/設定錯誤或 Heartbeats SDK 錯誤
   * ERROR - 指出重要的整合錯誤或 Heartbeats SDK 錯誤
* **tag**：發出記錄訊息的子元件的名稱 (通常是類別名稱)
* **message**：實際追蹤訊息

您可以使用 Media SDK 程式庫的記錄輸出驗證實作。在整個記錄中搜尋字串 `#track`，會是不錯的策略。這將會反白顯示應用程式呼叫的所有 `track*()`。

例如，這是篩選了 `#track` 之記錄的外觀：

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
