---
title: 在 Roku 上實作標準中繼資料
description: 說明如何設定在Roku上隨追蹤呼叫傳送的標準視訊和廣告中繼資料。
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Roku 上實作標準中繼資料{#implement-standard-metadata-on-roku}

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。

**影片:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**音訊:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

請在這裡參閱完整的視訊中繼資料清單: [音訊與視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)

