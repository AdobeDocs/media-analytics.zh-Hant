---
title: 了解如何在 Android 上實作標準廣告中繼資料
description: 如何在 Android 上將標準廣告中繼資料用於廣告追蹤。
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '63'
ht-degree: 100%

---

# 在 Android 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-android}

## 廣告常數

| 常數名稱 | 說明 |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 在「廣告 `MediaObject`」上附加標準廣告中繼資料的常數。 |

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典：

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
