---
title: 了解如何使用 JavaScript 3.x 實作標準廣告中繼資料
description: 如何在瀏覽器中使用 JavaScript 3.x 應用程式，於廣告追蹤中使用標準廣告中繼資料。
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 100%

---

# 使用 JavaScript 3.x 實作標準廣告中繼資料{#implement-standard-ad-metadata-on-javascript}

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典：

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
