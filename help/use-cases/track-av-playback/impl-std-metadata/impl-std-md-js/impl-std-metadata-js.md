---
title: 了解如何使用 JavaScript 2.x 實作標準中繼資料
description: 了解如何在瀏覽器應用程式 (JS 2.x) 中設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
exl-id: 889c294b-ac45-4e82-abb3-88ab70abbc3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NSSNy7QmJL4xmVs0rAzNlDh4U-skwd4PePPkk9vDXAM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 70
ht-degree: 100%

---

# 使用 JavaScript 2.x 實作標準中繼資料{#implement-standard-metadata-on-javascript}

## 中繼資料常數

| 常數名稱 | 說明   |
| --- | --- |
| `StandardMediaMetadata` | 用於在 `MediaObject` 上附加標準中繼資料的常數 |

## 實施

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。 例如：

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```
