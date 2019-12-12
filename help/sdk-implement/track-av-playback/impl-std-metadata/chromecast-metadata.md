---
title: Chromecast 中繼資料索引鍵
description: 說明如何在 Chromecast 上設定要連同追蹤呼叫一起傳送的標準視訊和廣告中繼資料。
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast 中繼資料索引鍵{#chromecast-metadata-keys}

標準視訊和廣告中繼資料可分別在媒體和廣告資訊物件上設定。在呼叫追蹤 API 之前，使用視訊/廣告中繼資料的常數索引鍵，設定包含資訊物件之標準中繼資料的字典。請參閱下列表格以獲取標準中繼資料常數的完整清單，然後是範例。

## 中繼資料常數 {#video-metadata-constants}

| 中繼資料名稱 | 內容資料索引鍵 | 常數名稱 |
| --- | --- | --- |
| 節目 | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| 季數 | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| 集數 | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| 資產 | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| 類型 | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| 首播日期 | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| 數位化首播日期 | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| 評等 | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| 創作者 | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| 網路 | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| 節目類型 | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| 廣告載入 | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| 已驗證 | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| 時段 | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| 動態消息 | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| 資料流格式 | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## 廣告中繼資料常數 {#ad-metadata-constants}

| 中繼資料名稱 | 內容資料索引鍵 | 常數名稱 |
| --- | --- | --- |
| 廣告商 | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| 行銷活動 ID | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| 創作 ID | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| 版面 ID | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| 網站 ID | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| 創作 URL | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Chromecast 實施範例 {#sample-implementations-for-chromecast}

### 影片

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### 音訊

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = “sample artist”; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### 廣告

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = “sample campaign”; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```

