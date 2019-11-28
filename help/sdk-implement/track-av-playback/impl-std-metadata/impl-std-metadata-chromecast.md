---
title: 在 Chromecast 上實作標準中繼資料
description: 說明如何在 Chromecast 上設定標準視訊和廣告中繼資料。
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 上實作標準中繼資料{#implement-standard-metadata-on-chromecast}

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。例如:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

請在這裡參閱完整的音訊和視訊中繼資料清單: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)。
