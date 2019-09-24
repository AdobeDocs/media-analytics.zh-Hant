---
description: 'null'
seo-description: 'null'
seo-title: 在 Android 上實作標準廣告中繼資料
title: 在 Android 上實作標準廣告中繼資料
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 Android 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-android}

## 廣告常數

| 常數名稱 | 說明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 在「廣告 `MediaObject`」上附加標準廣告中繼資料的常數。 |

## 實施標準廣告中繼資料

對於標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對的字典：

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

