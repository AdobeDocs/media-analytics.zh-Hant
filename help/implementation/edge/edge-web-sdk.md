---
title: 使用Adobe Experience Platform Web SDK傳送網頁資料給Edge
description: 瞭解如何使用Adobe Experience Platform Web SDK將Adobe串流媒體資料傳送到Experience Platform Edge。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ad40260d29bd5b739184cb551f084565d05e65a7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK傳送網頁資料給Edge

從2.20.0版開始， `streamingMedia` Adobe Experience Platform的元件 [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) 可讓您收集網站上與媒體工作階段相關的資料。 收集的資料可包括關於媒體播放、暫停、完成和其他相關事件的資訊。

收集資料後，您可以將其傳送至Adobe Experience Platform及/或Adobe Analytics以產生報表。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

對於使用Media JS SDK的客戶，Web SDK提供從Media JS SDK移轉至Web SDK的移轉路徑，同時支援現有的Media JS功能，例如處理媒體事件。

## 先決條件 {#prerequisites}

若要使用 `streamingMedia` 元件，您必須符合下列必要條件：

* 在您可以將Media Analytics資料傳送至Edge之前，請先完成中的步驟 [安裝Media Analytics與Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* 確保您有權存取Adobe Experience Platform和/或Adobe Analytics。
* 您必須使用Web SDK 2.20.0版或更新版本。 請參閱 [Web SDK安裝概述](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) 以瞭解如何安裝最新版本。
* 啟用 **[[!UICONTROL 媒體分析]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** 您正在使用的資料流選項。
* 確定您的資料流使用的結構描述包含媒體收集結構描述欄位。
* 在Web SDK設定中設定串流媒體功能，如本頁所示，可透過 [標籤延伸模組](#tag-extension) 或透過 [JavaScript資料庫](#library).

請依照本頁所述的步驟，將您的Analytics for Streaming Media實作從Media JS移轉至Web SDK。

### 步驟1：安裝Experience Platform Web SDK

請參閱 [專屬檔案](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) 以瞭解如何在您的Web屬性上安裝Web SDK。

### 步驟2：設定Web SDK `streamingMedia` 元件。

**範例**

以下程式碼片段顯示如何在Media JS中設定媒體收集。

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

您必須改為設定 `streamingMedia` Web SDK中的元件，如下例所示。

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

請參閱Web SDK `streamingMedia` 元件 [檔案](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) 以取得有關如何設定的完整詳細資訊。

### 步驟3：從Media JS SDK移轉時取得媒體追蹤器例項

對於使用Media JS SDK的客戶，Web SDK提供從Media JS SDK移轉至Web SDK的移轉路徑，同時支援現有的Media JS功能，例如處理媒體事件。

[!DNL Web SDK] 包含擷取Media Analytics追蹤器的命令。 您可以使用此命令來建立物件例項，然後使用與提供的相同API [Media JS程式庫](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)，追蹤媒體事件。

請參閱 [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) 檔案，以取得支援方法的完整詳細資料。

以下程式碼片段顯示如何在Media JS中擷取媒體追蹤器例項。

```javascript
var tracker = ADB.Media.getInstance();
```

請改用 `getMediaAnalyticsTracker` Web SDK中用於取得相同結果的命令，如下所示。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

所有的Helper方法都可在 `Media` 物件。 追蹤器例項提供追蹤器方法，如下所示。

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
