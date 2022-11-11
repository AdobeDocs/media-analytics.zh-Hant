---
title: 了解如何在iOS上實作標準廣告中繼資料
description: 如何在 iOS 上將標準廣告中繼資料用於廣告追蹤。
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 86%

---

# 在 iOS 上實施標準廣告中繼資料{#implement-standard-ad-metadata-on-ios}

## 廣告常數

| 常數名稱 | 說明 |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | 用於在 上附加標準廣告中繼資料的常數`AdInfo ADBMediaObject` |

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 中繼資料索引鍵](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
