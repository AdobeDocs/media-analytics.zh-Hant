---
title: 測試呼叫詳細資料
description: 探索驗證實作所必須進行的呼叫。
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 100%

---

# 測試呼叫詳細資料{#test-call-details}

## 啟動媒體播放器 {#start-the-media-player}

### Adobe Analytics (AppMeasurement) 開始呼叫 {#aa-start-call}

| 參數 |  值 (範例) |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | VOD |
| _**`custom.[value]`**_ | _**自訂中繼資料欄位**_ |
| _**`a.media.[value]`**_ | _**標準中繼資料欄位**_ |

**附註：**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 線性資料流的長度應設定為目前節目的最佳預估值。

### Adobe Analytics (AppMeasurement) 開始呼叫中的標準中繼資料 {#std-metadata-aa}

| 參數 |  值 (範例) |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics (AppMeasurement) 開始呼叫中的自訂中繼資料 {#custom-metadata-aa}

| 參數 |  值 (範例) |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics (心率) 開始呼叫 {#ma-start-call}

| 參數 |  值 (範例) |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**自訂中繼資料欄位**_ |
| _**`s:meta:a.media.[value]`**_ | _**標準中繼資料欄位**_ |

**附註：**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 視訊開始時的線性資料流播放點位置，應設定為目前節目開始後經過的秒數，而不是 0。

### Media Analytics (心率) 開始呼叫中的標準中繼資料 {#std-metadata-ma}

| 參數 |  值 (範例) |
|---|---|
| `s:meta:a.media.show` | 節目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics (心率) 開始呼叫中的自訂中繼資料 {#custom-metadata-ma}

| 參數 |  值 (範例) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (心率) Adobe Analytics 開始呼叫 {#ma-aa-start}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**附註：**

* 這個呼叫代表 Media SDK 已要求將 Adobe Analytics `pev2=ms_s` 呼叫傳送到 Adobe Analytics (AppMeasurement) 伺服器。
* 該呼叫不含自訂中繼資料。

## 檢視廣告播放 {#view-ad-playback}

### Adobe Analytics (AppMeasurement) 廣告開始呼叫 {#aa-ad-start-call}

| 參數 |  值 (範例) |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**中繼資料欄位**_ |
| _**`a.media.[value]`**_ | _**標準中繼資料欄位**_ |

**附註：**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 如果無法在廣告開始時取得廣告長度，可以設定為 -1。

### Adobe Analytics (AppMeasurement) 廣告開始呼叫中的標準中繼資料 {#std-metadata-aa-ad-start}

| 參數 |  值 (範例) |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics (AppMeasurement) 廣告開始呼叫中的自訂中繼資料 {#custom-metadata-aa-ad-start}

| 參數 |  值 (範例) |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (心率) 廣告開始呼叫 {#ma-ad-start-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**自訂中繼資料欄位**_ |
| _**`s:meta:a.media.[value]`**_ | _**標準中繼資料欄位**_ |

**附註：**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 如果無法在廣告開始時取得廣告長度，可以設定為 -1。

### Media Analytics (心率) 廣告開始呼叫中的標準中繼資料 {#std-metadata-ma-ad-start}

| 參數 |  值 (範例) |
|---|---|
| `s:meta:a.media.show` | 節目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics (心率) 廣告開始呼叫中的自訂中繼資料 {#custom-metadata-ma-ad-start}

| 參數 |  值 (範例) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (心率) Adobe Analytics 廣告開始呼叫 {#ma-aa-ad-start-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | 廣告 |

### Media Analytics (心率) 廣告播放呼叫 {#ma-ad-play-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (心率) 廣告暫停呼叫 {#ma-ad-pause-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (心率) Adobe Analytics 廣告完成呼叫 {#ma-aa-ad-complete-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

## 播放主要內容 {#play-main-content}

### Media Analytics (心率) 播放呼叫 {#ma-play-call}

| 參數 |  值 (範例) |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**附註：**

* 每個播放呼叫的播放點位置應該要以 10 秒為單位遞增。
* `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

## 暫停主要內容 {#pause-main-content}

### Media Analytics (心率) 暫停呼叫 {#ma-pause-call}

| 參數 |  值 (範例) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
