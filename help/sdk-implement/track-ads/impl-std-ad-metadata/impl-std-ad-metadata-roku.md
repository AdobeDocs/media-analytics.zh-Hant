---
title: 在 Roku 上實作標準廣告中繼資料
description: 如何在Roku的廣告追蹤中使用標準廣告中繼資料。
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Roku 上實作標準廣告中繼資料{#implement-standard-ad-metadata-on-roku}

## 實施標準廣告中繼資料

對於標準廣告中繼資料，請使用平台的索引鍵建立標準廣告中繼資料索引鍵值配對的字典：

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

