---
title: 使用JavaScript 2.x實作標準廣告中繼資料
description: 如何使用JavaScript 2.x應用程式，在瀏覽器中使用廣告追蹤中的標準廣告中繼資料。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

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
