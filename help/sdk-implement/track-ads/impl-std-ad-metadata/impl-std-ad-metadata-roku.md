---
title: 在 Roku 上實作標準廣告中繼資料
description: 如何在 Roku 上將標準廣告中繼資料用於廣告追蹤。
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Roku 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-roku}

## 實作標準廣告中繼資料

針對標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對字典:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

