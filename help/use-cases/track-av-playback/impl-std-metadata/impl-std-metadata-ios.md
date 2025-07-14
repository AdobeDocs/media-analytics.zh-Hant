---
title: 了解如何在 iOS 上實作標準中繼資料
description: 了解如何在 iOS 上設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# 在 iOS 上實作標準中繼資料{#implement-standard-metadata-on-ios}

## 中繼資料常數

| 常數名稱 | 說明 |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 用於在 `MediaInfo ADBMediaObject` 上附加標準中繼資料的常數 |

## 實作

1. 使用 `ADBStandardMetadataKeys`，建立標準中繼資料索引鍵值配對的字典。
   [iOS 中繼資料索引鍵](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. 對中繼資料使用標準中繼資料常數，在 `MediaInfo``ADBMediaObject` 例項上設定標準中繼資料字典。

1. 叫用 `MediaInfo` API 時，提供此 `trackSessionStart` 物件。

### 實作範例

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。例如：

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
