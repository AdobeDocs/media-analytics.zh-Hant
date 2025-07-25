---
title: 了解如何在 Chromecast 上實作標準中繼資料
description: 了解如何在 Chromecast 上設定標準視訊和廣告中繼資料
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# 在 Chromecast 上實作標準中繼資料{#implement-standard-metadata-on-chromecast}

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。例如：

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

請在這裡參閱完整的音訊和視訊中繼資料清單：[音訊和視訊參數](/help/implementation/variables/audio-video-parameters.md)。
