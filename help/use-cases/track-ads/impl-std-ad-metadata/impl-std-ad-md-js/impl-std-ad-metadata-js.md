---
title: 了解如何使用JavaScript 2.x實作標準廣告中繼資料
description: 如何在使用JavaScript 2.x應用程式的瀏覽器中，將標準廣告中繼資料用於廣告追蹤。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 54%

---

# 使用JavaScript 2.x實作標準廣告中繼資料{#implement-standard-ad-metadata-on-javascript}

## 廣告常數

| 常數名稱 | 說明 |
|---|---|
| `StandardAdMetadata` | 用於在 Ad Object 上附加標準廣告中繼資料的常數 |

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
