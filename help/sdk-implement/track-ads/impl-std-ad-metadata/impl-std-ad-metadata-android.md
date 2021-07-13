---
title: 了解如何在Android上實作標準廣告中繼資料
description: 如何在 Android 上將標準廣告中繼資料用於廣告追蹤。
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 86%

---

# 在 Android 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-android}

## 廣告常數

| 常數名稱 | 說明 |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 在「廣告 `MediaObject`」上附加標準廣告中繼資料的常數。 |

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
