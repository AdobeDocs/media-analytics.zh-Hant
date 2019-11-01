---
title: SDK 除錯
description: 本主題說明Media SDK中可用的追蹤／記錄。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# SDK 除錯{#sdk-debugging}

您可以啟用和停用記錄。 Media SDK提供廣泛的媒體追蹤堆疊追蹤／記錄機制。 You can enable or disable logging by setting the `debugLogging` flag on the Config object.

## 除錯記錄的程式碼範例

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS 應用程式

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

## 使用 Adobe Bloodhound 來測試 Chromecast 應用程式

在應用程式開發期間，Bloodhound 可讓您在本機檢視伺服器呼叫，以及選擇將資料轉送至 Adobe 收集伺服器。如需 Bloodhound 的詳細資訊，請參閱下列指南:

* [Mac 適用的 Bloodhound 3.x](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Windows 適用的 Bloodhound 2.2](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Adobe Bloodhound 已於 2017 年 4 月 30 日起停止服務。自 2017 年 5 月 1 日起，不再提供額外的增強功能、額外工程支援，或 Adobe Expert Care 支援。

## 日誌消息

記錄訊息會遵循此格式:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp**: 這是目前的 CPU 時間 (GMT 時區)
* **level**: 定義的訊息層次有 4 個:
   * INFO - 通常是來自應用程式的輸入資料 (驗證播放器名稱、視訊 ID 等等)
   * DEBUG - 除錯記錄檔，開發人員用來除錯更複雜的問題
   * WARN - 指出可能的整合/設定錯誤或 Heartbeats SDK 錯誤
   * ERROR - 指出重要的整合錯誤或 Heartbeats SDK 錯誤
* **tag**: 發出記錄訊息的子元件的名稱 (通常是類別名稱)
* **message**: 實際追蹤訊息

您可以使用Media SDK程式庫輸出的記錄檔來驗證實作。 良好的策略是搜尋整個記錄中是否有字串 `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

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

