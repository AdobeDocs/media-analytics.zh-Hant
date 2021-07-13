---
title: 了解如何在Android上實作標準中繼資料
description: 了解如何在Android上設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 76%

---

# 在 Android 上實作標準中繼資料{#implement-standard-metadata-on-android}

## 標準中繼資料常數

| 常數名稱 | 說明 |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | 用於在 `MediaObject` 上附加標準中繼資料的常數。 |

## 中繼資料索引鍵 API 參考資料

* 建立標準中繼資料索引鍵值配對的 `HashMap`。
   * [視訊中繼資料索引鍵](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [音訊中繼資料索引鍵](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* 對中繼資料使用標準中繼資料常數，在 `HashMap` 上設定標準視訊中繼資料 `MediaInfo`。
* 叫用 `MediaInfo` API 時，提供此 `trackSessionStart()` 物件。

## 實施範例

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
