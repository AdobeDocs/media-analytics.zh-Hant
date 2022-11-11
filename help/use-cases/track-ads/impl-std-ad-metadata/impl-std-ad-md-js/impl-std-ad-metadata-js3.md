---
title: 了解如何使用JavaScript 3.x實作標準廣告中繼資料
description: 如何在使用JavaScript 3.x應用程式的瀏覽器中，將標準廣告中繼資料用於廣告追蹤。
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 42%

---

# 使用JavaScript 3.x實作標準廣告中繼資料{#implement-standard-ad-metadata-on-javascript}

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
