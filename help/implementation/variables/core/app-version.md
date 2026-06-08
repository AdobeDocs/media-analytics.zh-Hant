---
title: 應用程式版本
description: 設定媒體播放器應用程式的版本字串。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---


# 應用程式版本

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**應用程式版本**變數的資料集合。 如需對應的報表維度，請參閱[應用程式版本](/help/reporting/dimensions/app-version.md)。*

>[!ENDSHADEBOX]

應用程式版本變數可識別您的媒體播放器應用程式的版本。 在SDK初始化期間設定一次；該值會自動包含在每個後續工作階段開始請求中。 使用符合應用程式發行週期的版本字串（例如，`"2.1.0"`或`"prod-YYYY-03-15"`）。

>[!NOTE]
>
>此欄位會擷取&#x200B;**媒體播放器應用程式**&#x200B;的版本，而非Adobe的SDK資料庫。 Adobe自己的SDK程式庫版本會作為個別的內部欄位自動收集。

| 屬性 | 價值 |
| --- | --- |
| **XDM集合欄位** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **媒體收集API引數** | `media.sdkVersion` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [工作階段開始](/help/implementation/events/session/session-start.md) |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)時，在`streamingMedia`設定物件中設定`appVersion`：

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

在初始化媒體追蹤器之前，在應用程式設定中設定`edgeMedia.appVersion`：

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

在初始化媒體追蹤器之前，在應用程式設定中設定`edgeMedia.appVersion`：

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku Edge]

使用`ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`在SDK設定中設定應用程式版本：

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB Media Edge API]

在[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)要求的`sessionDetails`物件中包含`appVersion`：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

呼叫`ADB.Media.configure`之前，先在`MediaConfig`物件上設定`appVersion`：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

在ADBMobile設定的`mediaHeartbeat`區段中設定`sdkVersion`。 此欄位會擷取您的播放器應用程式版本，而非Chromecast SDK程式庫版本。

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB Roku 2.x]

在`ADBMobileConfig.json`的`mediaHeartbeat`區段中設定`sdkVersion`。 此欄位會擷取您的播放器應用程式版本，而非Roku 2.x SDK程式庫版本：

```json
"mediaHeartbeat": {
  "sdkVersion": "2.1.0"
}
```

>[!TAB 媒體收集API]

在`sessionStart` POST要求的`params`物件中包含`media.sdkVersion`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API工作階段參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
