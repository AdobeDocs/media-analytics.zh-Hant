---
seo-title: 追蹤下載內容
title: 追蹤下載內容
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# 追蹤下載內容{#track-downloaded-content}

## 概述 {#section_hcy_3pk_cfb}

「下載的內容」功能可在使用者離線時追蹤媒體使用量。舉例來說，使用者在行動裝置上下載並安裝應用程式，然後使用應用程式將內容下載至裝置上的本機儲存。為了追蹤下載的資料，Adobe開發了「下載內容」功能。使用此功能，當使用者從裝置儲存空間播放內容時，不論裝置的連線為何，追蹤資料都會儲存在裝置上。當使用者完成播放作業時，裝置會在線上傳回，儲存的追蹤資訊會傳送至單一裝載內的Media Collection API後端。從這裡開始，處理和報告在媒體收集API中會正常運作。

對比這兩種方法：

* 線上

   透過此即時方式，媒體播放器會在每個播放器事件上傳送追蹤資料，並每10秒傳送網路ping(每秒一秒)到後端。

* 離線(已下載的內容功能)

   透過此批次處理方法，必須產生相同的工作階段事件，但會儲存在裝置上，直到將它們傳送至後端作為單一作業(請參閱下方範例)。

每個方法都有其優點和缺點：
* 線上腳本會即時追蹤；這需要在每個網路呼叫之前進行連線檢查。
* 離線藍本(已下載內容功能)只需要一個網路連線檢查，但是裝置上也需要較大的記憶體。

## 實施 {#section_jhp_jpk_cfb}

### 事件結構

「下載內容」功能只是線上媒體收集API的離線版本，因此您的播放器批次資料並傳送至後端的事件資料必須使用您在進行線上呼叫時所使用的相同事件結構。如需這些結構描述的詳細資訊，請參閱：
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 批次裝載中的第一個事件必須與Media Collection API `sessionStart` 一樣正常。
* **您必須加入`media.downloaded: true`** 事件的標準中繼資料參數(`params``sessionStart` 索引鍵)中，向後端指出您要傳送下載內容。如果在傳送下載資料時此參數不存在或設為false，API將傳回400個回應代碼(不當請求)。此參數會將下載與即時內容區分為後端。(Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* 實施時應負責依照其外觀的順序，正確地儲存播放器事件。

### 回應代碼

* 201 - Created: Successful Request；資料有效，工作階段已建立且將進行處理。
* 400 - Bad Request；結構驗證失敗，已捨棄所有資料，不會處理任何工作階段資料。

## 與 Adobe Analytics 整合 {#section_cty_kpk_cfb}

計算Analytics啓動/關閉所下載內容藍本的呼叫時，後端會為已接收的第一個和最後一個事件(開始和完成)設定時間戳記，稱為 `ts.` 時間戳記。此機制可讓已完成的媒體工作階段放置在正確的時間點(亦即，即使使用者未在線上返回數天，媒體會話也會回報為實際檢視內容時發生)。您必須透過建立&#x200B;_可選時間戳記報表套裝，以在 Adobe Analytics 端啟用此機制。_ 若要啓用時間戳記可選報表套裝，請參閱 [可選時間戳記。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## 範例工作階段比較 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### 線上內容

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### 下載的內容

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

