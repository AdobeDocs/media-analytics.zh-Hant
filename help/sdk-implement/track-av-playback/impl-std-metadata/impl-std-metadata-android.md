---
description: 'null'
seo-description: 'null'
seo-title: 在 Android 上實作標準中繼資料
title: 在 Android 上實作標準中繼資料
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# 在 Android 上實作標準中繼資料{#implement-standard-metadata-on-android}

## 標準中繼資料常數

| 常數名稱 | 說明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | 用於在 `MediaObject` 上附加標準中繼資料的常數。 |

## 中繼資料金鑰API參考

* 建立標準 `HashMap` 中繼資料索引鍵值配對。
   * [視訊中繼資料金鑰](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [音訊中繼資料索引鍵](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* 對中繼資料使用標準中繼資料常數，在 `HashMap` 上設定標準視訊中繼資料 `MediaInfo`。
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## 實作範例

### 影片

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### 音訊

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
