---
title: Media Edge API資料對應和平台驗證
description: 瞭解哪些Media Edge API事件會在Adobe Experience Platform中產生Experience事件，以及如何使用mediaReporting XDM結構描述驗證您的實施。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 764
ht-degree: 4%

---


# Media Edge API資料對應和平台驗證

當您使用Media Edge API或Media Edge SDK傳送媒體追蹤事件時，Media Analytics後端會處理這些事件，並將運算後的體驗事件寫入Adobe Experience Platform資料集。 瞭解哪些事件可觸及Platform，以及後端為您計算的內容，可協助您驗證實作，並在Customer Journey Analytics或Adobe Analytics中建立準確的報告。

Media Edge使用兩個不同的XDM結構描述：

| 結構描述 | 命名空間 | 方向 | 用途 |
|---|---|---|---|
| 媒體收集 | `xdm.mediaCollection` | 使用者端Adobe | 您的播放器會傳送每個追蹤事件的內容 |
| 媒體報告 | `xdm.mediaReporting` | Adobe → Platform | 後端在處理後寫入資料集的內容 |

在`mediaReporting`中出現但您的`mediaCollection`裝載中沒有的欄位是&#x200B;**後端計算** — 衍生自工作階段中的完整事件序列。 您絕不會傳送這些欄位，因為Adobe會產生這些欄位。

## 寫入Platform資料集的事件

在12種可追蹤的事件型別中，只有5種會產生將個別體驗事件寫入資料集的作業：

| 事件型別 | 包含在資料集中 | 附註 |
|---|---|---|
| [工作階段開始](/help/implementation/events/session/session-start.md) | 是 | 在工作階段初始化時寫入 |
| [廣告開始](/help/implementation/events/ads/ad-start.md) | 是 | 在個別廣告開始時寫入 |
| [廣告完成](/help/implementation/events/ads/ad-complete.md) | 是 | 在廣告播放至完成時寫入 |
| [章節完成](/help/implementation/events/chapters/chapter-complete.md) | 是 | 章節播放至完成時寫入 |
| [工作階段完成](/help/implementation/events/session/session-complete.md) | 是 | 在工作階段結束時寫入；最豐富的計算欄位集 |
| [播放](/help/implementation/events/playback/play.md) | 否 | 用於計算`timePlayed` |
| [暫停開始](/help/implementation/events/playback/pause-start.md) | 否 | 用於計算`pauseCount`和`pauseTime` |
| [Ping](/help/implementation/events/playback/ping.md) | 否 | 心率；用於偵測工作階段閒置 |
| [緩衝開始](/help/implementation/events/playback/buffer-start.md) | 否 | 用於計算QoE緩衝量度 |
| [位元速率變更](/help/implementation/events/playback/bitrate-change.md) | 否 | 用於計算QoE位元速率量度 |
| [狀態開始](/help/implementation/events/player-state/state-start.md) | 否 | 用於運算播放器狀態量度 |
| [錯誤](/help/implementation/events/error.md) | 否 | 用於計算QoE中的`errorCount` |

## 後端計算欄位

下列欄位會顯示在`mediaReporting`裝載中，但絕不會成為集合裝載的一部分。 後端會從完整事件序列衍生它們。

**工作階段層級** （出現在`sessionComplete`）：

| 欄位 | 說明 |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | 主要內容播放的總秒數，不包括廣告 |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | 經過的總秒數，包括廣告 |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | 刪除重複資料秒數 — 多次檢視的間隔只會計算一次 |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed`除以內容長度 |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | 預估並行串流 |
| `xdm.mediaReporting.sessionDetails.adCount` | 開始的廣告數量 |
| `xdm.mediaReporting.sessionDetails.chapterCount` | 開始的章節數 |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | 暫停頻率和總暫停期間 |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | 進度里程碑標幟(10%、25%、50%、75%、95%) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | 是否檢視了至少一個內容框架 |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | 完成和開始旗標 |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | 上次ping與工作階段關閉之間的時間 |
| `xdm.mediaReporting.sessionDetails.segment` | 內容區段括弧（例如， `[0-1]`） |

**廣告層級** （出現在`adComplete`）：

| 欄位 | 說明 |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | 播放廣告內容的秒數 |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | 廣告是否播放至完成 |

**章節層級** （出現在`chapterComplete`）：

| 欄位 | 說明 |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | 章節內容播放的秒數 |
| `xdm.mediaReporting.chapterDetails.isCompleted` | 章節是否播放至完成 |
| `xdm.mediaReporting.chapterDetails.isStarted` | 章節是否開始 |

**QoE** （彙總於`sessionComplete`）：

| 欄位 | 說明 |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | 整個工作階段的平均位元速率 |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | 分段平均位元速率範圍 |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | 位元速率變更的數量 |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | 錯誤數 |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | 掉格總數 |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | 播放器錯誤碼陣列 |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 是否發生任何錯誤 |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 是否發生掉格 |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 是否發生位元速率變更 |

## 下載內容

對於使用[下載的端點](/help/use-cases/track-downloaded-content.md)追蹤的工作階段，後端會在`sessionStart`報告事件上自動將`xdm.mediaReporting.sessionDetails.isDownloaded`設定為`true`。 下載工作階段的所有其他報表事件都會遵循與即時工作階段相同的結構。 在CJA或Adobe Analytics中使用此欄位來篩選或區分下載的播放。

如需集合實作詳細資料，請參閱Media Edge API參考中的[已下載端點](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/)。

## 驗證實作

透過Media Edge API傳送事件後，請使用下列其中一種方法，驗證您的資料正確著陸：

**Adobe Experience Platform資料集預覽**

1. 在[CX Enterprise](https://experience.adobe.com)中，導覽至&#x200B;**[!UICONTROL 資料集]**&#x200B;並選取您的串流媒體資料集。
2. 選取&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以檢視最近擷取的體驗事件。
3. 確認`eventType`值（例如`media.sessionStart`和`media.sessionComplete`）顯示有已填入的`mediaReporting`欄位。

**Customer Journey Analytics資料集檢查**

1. 在CJA中，開啟與串流媒體資料集相關聯的連線。
2. 選取&#x200B;**新增資料集**&#x200B;並檢查結構描述，以確認`mediaReporting`欄位已對應到預期的維度和量度。

**Adobe Analytics處理規則（如果使用Analytics目的地）**

對於透過Adobe Analytics來源聯結器接收資料的Analytics報表套裝，您可以使用處理規則將`mediaReporting`個內容資料變數對應至自訂prop或eVar。 `isDownloaded`旗標可用作`a.media.downloaded`。

## XDM裝載範例

下列範例顯示寫入至Platform資料集的每個報告事件的完整`mediaReporting` XDM結構。 `_{tenantName}`屬性代表您組織任何自訂欄位的租使用者名稱空間。

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart （下載內容）

使用[下載的端點](/help/use-cases/track-downloaded-content.md)追蹤的工作階段會遵循相同的報告結構描述，但有一個關鍵差異： `sessionStart`報告事件上的`xdm.mediaReporting.sessionDetails.isDownloaded`設定為`true`。 所有其他事件型別則與上述即時內容範例相同。

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
