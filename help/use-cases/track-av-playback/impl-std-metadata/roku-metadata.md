---
title: 說明 Roku 中繼資料索引鍵
description: 了解可用的 Roku 中繼資料索引鍵，並查看標準中繼資料常數的完整清單。
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 91%

---

# Roku 中繼資料索引鍵{#roku-metadata-keys}

標準視訊、音訊和廣告中繼資料可分別在媒體和廣告資訊物件上設定。在呼叫追蹤 API 之前，使用視訊/廣告中繼資料的常數索引鍵，設定包含資訊物件之標準中繼資料的字典。請參閱下列表格以獲取標準中繼資料常數的完整清單，然後是範例。

## 視訊中繼資料常數 {#video-metadata-constants}

| 中繼資料名稱 | 內容資料索引鍵 | 常數名稱 |
| --- | --- | --- |
| 節目 | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| 季數 | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| 集數 | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| 資產 | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| 類型 | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| 首播日期 | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| 數位化首播日期 | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| 評等 | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| 創作者 | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| 網路 | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| 節目類型 | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| 廣告載入 | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| 已驗證 | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| 時段 | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| 動態消息 | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| 資料流格式 | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## 音訊中繼資料常數 {#audio-metadata-constants}

| 中繼資料名稱 | 內容資料索引鍵 | 常數名稱 |
| --- | --- | --- |
| 藝人 | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| 專輯 | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| 標籤 | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| 作者 | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| 電台 | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| 發行者 | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## 廣告中繼資料常數 {#ad-metadata-constants}

| 中繼資料名稱 | 內容資料索引鍵 | 常數名稱 |
| --- | --- | --- |
| 廣告商 | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| 行銷活動 ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| 創作 ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| 版面 ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 網站 ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 創作 URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## 常數 {#constants}

您可以使用下列常數來追蹤媒體事件：

### 其他常數

| 常數 | 說明 |
|---|---|
| `ERROR_SOURCE_PLAYER` | 錯誤來源的常數為播放器 |

### MediaObjectkey 常數 (用於作為 MediaObject 例項內的索引鍵)

| 常數 | 說明 |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | 可在 `MediaInfo` `trackLoad` 上設定中繼資料的常數 |
| `MEDIA_STANDARD_AD_METADATA` | 可在 `EventData` `trackEvent` 上設定廣告中繼資料的常數 |
| `MEDIA_RESUMED` | 傳送影片繼續心率的常數。如要延續先前暫停內容繼續影片追蹤，您必須在您呼叫 `MEDIA_RESUMED` 時設定在 `mediaInfo` 物件上的 `mediaTrackLoad` 屬性。（`MEDIA_RESUMED`不是您可以使用`mediaTrackEvent` API追蹤的事件。）當應用程式想要繼續追蹤使用者停止觀看但現在打算繼續觀看的內容時，`MEDIA_RESUMED`應設為true。 <br/><br/> 例如，假設使用者觀看了 30% 的內容，然後關閉該應用程式。這會導致作業結束。稍後，如果同一位使用者返回觀看同一個內容，而應用程式允許使用者從中斷的地方繼續，則應用程式應將 `MEDIA_RESUMED` 設定為「true」，同時呼叫 `mediaTrackLoad` API。結果是針對相同影片內容的這兩個不同媒體工作階段可以連結在一起。以下為實作範例： <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)`<br/><br/>這將會為該影片建立一個新的工作階段，但也會導致 SDK 傳送含有「繼續」事件類型的心率要求，其可用於報表，以將兩個不同的媒體工作階段繫結在一起。 |

### 內容類型常數

| 常數 | 說明 |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | LIVE 資料流類型常數 |
| `MEDIA_STREAM_TYPE_VOD` | VOD 資料流類型的常數 |

### 事件類型常數 (用於 trackEvent 呼叫)

| 常數 | 說明 |
|---|---|
| `MEDIA_BUFFER_START` | 緩衝區開始的事件類型 |
| `MEDIA_BUFFER_COMPLETE` | 緩衝區完成的事件類型 |
| `MEDIA_SEEK_START` | 搜尋開始的事件類型 |
| `MEDIA_SEEK_COMPLETE` | 搜尋完成的事件類型 |
| `MEDIA_BITRATE_CHANGE` | 位元速率變更的事件類型 |
| `MEDIA_CHAPTER_START` | 章節開始的事件類型 |
| `MEDIA_CHAPTER_COMPLETE` | 章節完成的事件類型 |
| `MEDIA_CHAPTER_SKIP` | 廣告開始的事件類型 |
| `MEDIA_AD_BREAK_START` | 廣告開始的事件類型 |
| `MEDIA_AD_BREAK_COMPLETE` | 廣告插播完成的事件類型 |
| `MEDIA_AD_BREAK_SKIP` | 廣告插播略過的事件類型 |
| `MEDIA_AD_START` | 廣告開始的事件類型 |
| `MEDIA_AD_COMPLETE` | 廣告完成的事件類型 |
| `MEDIA_AD_SKIP` | 廣告略過的事件類型 |
