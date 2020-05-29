---
title: 使用JavaScript 3.x實作標準中繼資料
description: 說明如何在瀏覽器應用程式 (JS) 中設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# 使用JavaScript 3.x實作標準中繼資料{#implement-standard-metadata-on-javascript}

## 實作

實例化上下文資料物件，填入所需的標準中繼資料變數。 例如：

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
