---
description: 'null'
seo-description: 'null'
seo-title: 在 iOS 上實作標準中繼資料
title: 在 iOS 上實作標準中繼資料
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 上實作標準中繼資料{#implement-standard-metadata-on-ios}

## 中繼資料常數

| 常數名稱 | 說明   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constant for attaching standard metadata on `MediaInfo ADBMediaObject` |

## 實施

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [IOS中繼資料金鑰](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. 對中繼資料使用標準中繼資料常數，在 `MediaInfo``ADBMediaObject`   例項上設定標準中繼資料字典。

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### 以下是實作範例

在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。例如:

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

