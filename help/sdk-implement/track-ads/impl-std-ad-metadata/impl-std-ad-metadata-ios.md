---
description: 'null'
seo-description: 'null'
seo-title: 在 iOS 上實作標準廣告中繼資料
title: 在 iOS 上實作標準廣告中繼資料
uuid: f15fb727-5a5b-46c5-bf12-93b376 c10 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 iOS 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-ios}

## 廣告常數

| 常數名稱 | 說明   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## 實作標準廣告中繼資料

對於標準廣告中繼資料，請使用您平台的索引鍵建立標準廣告中繼資料索引鍵值配對的字典：

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 中繼資料索引鍵](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
