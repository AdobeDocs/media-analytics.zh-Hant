---
title: 了解如何在 Roku 上實作標準中繼資料
description: 了解如何在 Roku 上設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# 在 Roku 上實作標準中繼資料{#implement-standard-metadata-on-roku}

例項化標準中繼資料物件、填入所需的變數，並在媒體心率物件上設定中繼資料物件。

**影片：**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

**音訊：**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

請在這裡參閱完整的視訊中繼資料清單：[音訊和視訊參數](/help/implementation/variables/audio-video-parameters.md)
