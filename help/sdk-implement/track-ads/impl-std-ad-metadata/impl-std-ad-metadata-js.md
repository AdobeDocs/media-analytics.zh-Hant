---
title: 在 JavaScript 上實作標準廣告中繼資料
description: 如何在瀏覽器(JS)應用程式中的廣告追蹤中使用標準廣告中繼資料。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-javascript}

## 廣告常數

| 常數名稱 | 說明   |
|---|---|
| `StandardAdMetadata` | 用於在 Ad Object 上附加標準廣告中繼資料的常數 |

## 實施標準廣告中繼資料

對於標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對的字典：

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

