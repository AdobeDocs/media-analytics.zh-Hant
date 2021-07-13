---
title: 了解如何在Roku上實作標準中繼資料
description: 了解如何在Roku上設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 61%

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

請在這裡參閱完整的視訊中繼資料清單: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)
