---
title: JavaScript 3.x Media SDK API參考
description: Media SDK JavaScript 3.x （ADB.Media和ADB.MediaConfig類別）的API參考。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# JavaScript 3.x Media SDK API參考

>[!BEGINSHADEBOX]

本頁涵蓋僅限Analytics的JavaScript 3.x SDK。 如需建議的實作，請參閱[使用Edge Network實作串流媒體](/help/implementation/edge/edge-web-sdk.md)。

>[!ENDSHADEBOX]

## ADB.Media

### 靜態方法

+++configure

設定MediaSDK以進行追蹤。 在頁面中建立任何追蹤器例項前，應呼叫此方法一次。

**語法**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| 變數名稱 | 類型 | 說明 |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | 有效的媒體設定 |
| `appMeasurement` | 物件 | AppMeasurement執行個體 |

**範例**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

建立媒體例項以追蹤播放工作階段。 若在設定媒體之前呼叫，則傳回`null`。

**語法**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| 變數名稱 | 類型 | 必要 | 說明 |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | 追蹤器設定 | 否 | 追蹤器設定物件。 |

**範例**

```javascript
var tracker = ADB.Media.getInstance();
```

若要覆寫每個追蹤器執行個體的`channel`或`playerName`，請在追蹤器設定物件中傳遞覆寫值。

**追蹤器組態範例**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

建立包含媒體資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `name` | 字串 | 表示媒體名稱的非空白字串 |
| `id` | 字串 | 表示唯一媒體識別碼的非空白字串 |
| `length` | 數字 | 表示媒體秒數長度的正數。 如果長度未知，請使用`0`。 |
| `streamType` | 字串 | 資料流型別或非空白字串來代表媒體資料流型別。 |
| `mediaType` | 媒體型別 | 媒體型別（音訊或視訊） |

**範例**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createadbreakobject

建立包含廣告插播資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `name` | 字串 | 表示廣告插播名稱（前段、中段和後段）的非空白字串 |
| `position` | 數字 | 內容中廣告插播的編號位置從1開始 |
| `startTime` | 數字 | 廣告插播開始時的播放點值。 |

**範例**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

建立包含廣告資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `name` | 字串 | 表示廣告名稱的非空白字串 |
| `id` | 字串 | 表示廣告ID的非空白字串 |
| `position` | 數字 | 廣告插播中的廣告編號位置從1開始 |
| `length` | 數字 | 表示廣告長度的正數 |

**範例**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

建立包含章節資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `name` | 字串 | 表示章節名稱的非空白字串 |
| `position` | 數字 | 內容中章節的位置，從1開始 |
| `length` | 數字 | 表示章節長度的正數 |
| `startTime` | 數字 | 章節開頭的播放點值 |

**範例**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

建立包含狀態資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createStateObject(name)
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `name` | 字串 | 播放器狀態或非空白字串，表示狀態名稱 |

**範例**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

建立包含QoE資訊的物件。 如果傳遞無效的引數，則傳回空白物件。

**語法**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| 變數名稱 | 類型 | 說明 |
| :--- | :--- | :--- |
| `bitrate` | 數字 | 表示目前位元速率的正數（如果未知，則為0） |
| `startupTime` | 數字 | 表示啟動時間的正數（如果未知，則為0） |
| `fps` | 數字 | 表示目前FPS的正數（如果未知，則為0） |
| `droppedFrames` | 數字 | 表示掉格的正數（如果未知，則為0） |

**範例**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

傳回MediaSDK版本。

**語法**

```javascript
ADB.Media.version
```

**範例**

```javascript
console.log(ADB.Media.version);
```

+++

### 執行個體方法

+++trackSessionStart

追蹤開始播放的意圖。 這會在媒體追蹤器例項上啟動追蹤工作階段。 另請參閱媒體繼續。

**語法**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| 變數名稱 | 說明 | 必填 |
| :--- | :--- | :---: |
| `mediaObject` | 使用`createMediaObject`方法建立的媒體資訊。 | 是 |
| `contextData` | 選用的媒體內容資料。 對於標準中繼資料索引鍵，請使用標準視訊常數或標準音訊常數。 | 否 |

**範例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

追蹤媒體播放或在上次暫停後繼續。

**語法**

```javascript
ADB.Media.trackPlay();
```

**範例**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

追蹤媒體暫停。

**語法**

```javascript
ADB.Media.trackPause();
```

**範例**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

追蹤媒體完成。 只有在媒體已完整檢視後，才呼叫此方法。

**語法**

```javascript
ADB.Media.trackComplete();
```

**範例**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

追蹤檢視工作階段的結尾。 即使使用者未檢視媒體至完成，仍呼叫此方法。

**語法**

```javascript
ADB.Media.trackSessionEnd();
```

**範例**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

追蹤媒體播放中的錯誤。

**語法**

```javascript
ADB.Media.trackError(errorId);
```

| 變數名稱 | 說明 | 必填 |
| :--- | :--- | :---: |
| `errorId` | 包含錯誤資訊的非空白字串 | 是 |

**範例**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

追蹤媒體事件的方法。

| 變數名稱 | 說明 |
| :--- | :--- |
| `event` | 媒體事件 |
| `info` | 對於`AdBreakStart`事件，廣告插播資訊是使用`createAdBreakObject`方法所建立。 對於`AdStart`事件，廣告資訊是使用`createAdObject`方法所建立。 對於`ChapterStart`事件，使用`createChapterObject`方法建立章節資訊。 對於`StateStart`和`StateEnd`事件，狀態資訊是使用`createStateObject`方法所建立。 其他事件則不需要這個選項。 |
| `contextData` | 可為`AdStart`和`ChapterStart`事件提供選擇性內容資料。 其他事件則不需要這個選項。 |

**語法**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**範例**

**追蹤廣告插播**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**追蹤廣告**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**追蹤章節**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**追蹤狀態**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**追蹤播放事件**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**追蹤位元速率變更**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

提供目前的媒體播放點給媒體追蹤器。 如需精確追蹤，請在播放期間播放點變更時呼叫此方法。

**語法**

```javascript
ADB.Media.updatePlayhead(time);
```

| 變數名稱 | 說明 |
| :--- | :--- |
| `time` | 目前的播放點（以秒為單位）。 對於隨選影片(VOD)，此值是從媒體專案的開頭開始以秒為單位指定的。 對於直播串流，如果播放器未提供內容持續時間的相關資訊，則此值可以指定為自當天UTC午夜開始的秒數。 注意：使用進度標記時，需要內容持續時間，並且播放點需要更新為從媒體項目開始的秒數，從 0 開始。 |

**範例**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

為媒體追蹤器提供目前的QoE資訊。 為精確追蹤，當媒體播放器提供更新的QoE資訊時，請多次呼叫此方法。

**語法**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| 變數名稱 | 說明 |
| :--- | :--- |
| `qoeObject` | 使用`createQoEObject`方法建立的目前QoE資訊。 |

**範例**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++銷毀

摧毀追蹤器例項。

**語法**

```javascript
ADB.Media.destroy();
```

**範例**

```javascript
tracker.destroy();
```

+++

### 常數

+++追蹤器設定

定義每個追蹤器例項可設定的設定金鑰。

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++媒體型別

定義目前追蹤的媒體型別。

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++資料流類型

定義目前追蹤內容的資料流型別。

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++標準中繼資料索引鍵

`ADB.Media.VideoMetadataKeys`、`ADB.Media.AudioMetadataKeys`和`ADB.Media.AdMetadataKeys`提供標準中繼資料的內容資料索引鍵字串。 如需索引鍵及其對應報表變數的完整清單，請參閱[標準中繼資料變數參考](/help/implementation/variables/standard-metadata/show.md)。

+++

+++媒體事件

定義追蹤事件的型別。

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++播放器狀態

定義追蹤播放器狀態的標準值。

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++媒體繼續

常數，表示目前的追蹤工作階段正在繼續先前關閉的工作階段。 啟動追蹤工作階段時，必須提供此資訊。

**語法**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**範例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| 索引鍵 | 必要 | 說明 |
| :--- | :--- | :--- |
| `trackingServer` | 是 | 輸入下載的媒體追蹤資料應該傳送到的媒體收集API伺服器名稱。 請聯絡您的Adobe客戶代表以接收此資訊。 |
| `channel` | 否 | 管道名稱屬性 |
| `playerName` | 否 | 使用中的媒體播放器名稱 |
| `appVersion` | 否 | 輸入媒體播放器應用程式的版本/SDK |
| `debugLogging` | 否 | 啟用或停用Media SDK記錄（預設值： `false`） |
| `ssl` | 否 | 透過SSL傳送ping （預設值： `true`） |
