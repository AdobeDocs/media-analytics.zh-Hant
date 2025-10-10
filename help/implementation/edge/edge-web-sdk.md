---
title: 使用Adobe Experience Platform Web SDK將網頁資料傳送至Edge
description: 瞭解如何使用Adobe Web SDK將Adobe Experience Platform串流媒體資料傳送到Experience Platform Edge。
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 使用Adobe Experience Platform Web SDK將網頁資料傳送至Edge

從2.20.0版開始，Adobe Experience Platform `streamingMedia`Web SDK[的](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/home)元件可讓您收集與網站上的媒體工作階段相關的資料。 收集的資料可包括關於媒體播放、暫停、完成和其他相關事件的資訊。

收集資料後，您可以將其傳送至Adobe Experience Platform及/或Adobe Analytics以產生報表。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

對於使用Media JS SDK的客戶，Web SDK提供從Media JS SDK移轉至Web SDK的移轉路徑，同時支援現有的Media JS功能，例如處理媒體事件。

## 先決條件 {#prerequisites}

若要使用Web SDK的`streamingMedia`元件，您必須符合下列必要條件：

* 在將串流媒體資料傳送到Edge之前，請先使用Edge Network[完成](/help/implementation/edge/implementation-edge.md)實作Adobe串流媒體服務中的步驟。
* 確保您有權存取Adobe Experience Platform和/或Adobe Analytics。
* 您必須使用Web SDK 2.20.0版或更新版本。 請參閱[網頁SDK安裝概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/install/overview)，瞭解如何安裝最新版本。
* 為您使用的資料流啟用&#x200B;**[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/datastreams/configure)**&#x200B;選項。
* 確定您的資料流使用的結構描述包含媒體收集結構描述欄位。
* 透過[標籤擴充功能](#tag-extension)或透過[JavaScript資料庫](#library)，設定網頁SDK組態中的串流媒體服務（如本頁所示）。

請依照本頁所述的步驟，將串流媒體服務實作從Media JS移轉至Web SDK。

### 步驟1：安裝Experience Platform Web SDK

請參閱[專屬檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/install/overview)，瞭解如何在您的Web屬性上安裝Web SDK。

### 步驟2：設定網頁SDK `streamingMedia`元件。

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

您而是必須在Web SDK中設定`streamingMedia`元件，如下例所示。

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

如需如何設定的完整詳細資訊，請參閱網頁SDK `streamingMedia`元件[檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/commands/configure/streamingmedia)。

### 步驟3：從Media JS SDK移轉時取得Media追蹤器例項

對於使用Media JS SDK的客戶，Web SDK提供從Media JS SDK移轉至Web SDK的移轉路徑，同時支援現有的Media JS功能，例如處理媒體事件。

[!DNL Web SDK]包含擷取Media Analytics追蹤器的命令。 您可以使用此命令來建立物件執行個體，然後使用與[Media JS程式庫](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)提供的相同API來追蹤媒體事件。

請參閱[`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker)檔案，以取得支援方法的完整詳細資料。

以下程式碼片段顯示如何在Media JS中擷取媒體追蹤器例項。

```javascript
var tracker = ADB.Media.getInstance();
```

請改用Web SDK中的`getMediaAnalyticsTracker`命令來取得相同的結果，如下所示。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

所有協助程式方法都可在`Media`物件上使用。 追蹤器例項提供追蹤器方法，如下所示。

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
