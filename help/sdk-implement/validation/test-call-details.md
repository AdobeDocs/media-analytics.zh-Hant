---
seo-title: 測試呼叫詳細資料
title: 測試呼叫詳細資料
uuid: d3a0e62f-2fc3-413d-ac56-adbhone9 b3 e983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 測試呼叫詳細資料{#test-call-details}

## 啟動視訊播放器 {#section_qts_xff_f2b}

### 媒體分析開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | VOD |
| `custom.[value]` | 自訂中繼資料欄位 |
| `a.media.[value]` | 標準中繼資料欄位 |

**附註:**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 線性資料流的長度應設定為目前節目的最佳預估值。

### Media Analytics中的標準中繼資料開始呼叫

| 參數 | 值 (範例)   |
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

### 心率開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | 自訂中繼資料欄位 |
| `s:meta:a.media.[value]` | 標準中繼資料欄位 |

### 媒體分析中的媒體中繼資料開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**附註:**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 視訊開始時的線性資料流播放點位置，應設定為目前節目開始後經過的秒數，而不是 0。

### Heartbeat Analytics 開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

### 心率開始呼叫中的媒體中繼資料

| 參數 | 值 (範例)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 心率開始呼叫中的標準中繼資料

| 參數 | 值 (範例)   |
|---|---|
| `s:meta:a.media.show` | Show |
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

**附註:**

* 這個呼叫代表心率程式庫已要求將 analytics pev2=ms_s 呼叫傳送到 Analytics 伺服器。
* 該呼叫不含自訂中繼資料。

## 檢視廣告播放 {#section_wz3_yff_f2b}

### 媒體分析廣告開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | True |
| `custom.[value]` | 中繼資料欄位 |
| `a.media.[value]` | 標準中繼資料欄位 |

**注意:** 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。

### 心率廣告開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | 自訂中繼資料欄位 |
| `s:meta:a.media.[value]` | 標準中繼資料欄位 |

### 媒體分析廣告開始呼叫中的媒體中繼資料

| 參數 | 值 (範例)   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics廣告開始呼叫中的標準中繼資料

| 參數 | 值 (範例)   |
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

**附註:**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 如果無法在廣告開始時取得廣告長度，可以設定為 -1。

### Heartbeat Analytics 廣告開始呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

### 心率廣告開始呼叫中的媒體中繼資料

| 參數 | 值 (範例)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 心率廣告開始呼叫中的標準中繼資料

| 參數 | 值 (範例)   |
|---|---|
| `s:meta:a.media.show` | Show |
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

**附註:**

* 應該要有其他內容資料變數，而且應該要含有中繼資料。請參閱以下中繼資料詳情。
* 如果無法在廣告開始時取得廣告長度，可以設定為 -1。

### 心率廣告完成呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

### 心率廣告播放呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

## 播放主要內容 {#section_u1l_1gf_f2b}

### 心率播放呼叫

| 參數 | 值 (範例)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**附註:**

* 每個播放呼叫的播放點位置應該要以 10 為單位遞增。
* `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

