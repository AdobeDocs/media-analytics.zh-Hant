---
title: 了解如何使用JavaScript 3.x實作標準中繼資料
description: 了解如何在瀏覽器應用程式(JS 3.x)中設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 10%

---

# 使用JavaScript 3.x實作標準中繼資料{#implement-standard-metadata-on-javascript}

## 實作

實例化內容資料物件，填入所需的標準中繼資料變數。 例如：

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
