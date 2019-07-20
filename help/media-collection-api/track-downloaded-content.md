---
seo-title: 追蹤下載內容
title: 追蹤下載內容
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: 501bbfe8b44a2a8e9b2ac2caab49b2317f9ea0f3

---


# 追蹤下載內容{#track-downloaded-content}

## 概述 {#section_hcy_3pk_cfb}

Downloaded Content API 提供可在使用者離線時追蹤媒體消耗的功能。舉例來說，使用者在行動裝置上下載並安裝應用程式，然後使用應用程式將內容下載至裝置上的本機儲存。Adobe 已開發 Downloaded Content API 以追蹤此下載資料。透過此 API，當使用者從裝置的儲存播放內容時，無論裝置是否連線，追蹤資料都會儲存在裝置上。當使用者完成播放作業，而裝置上線時，儲存的追蹤資訊會傳送至單一裝載內的Media Collection API後端。在那裡，處理和報告程序會在該 API 所依據的媒體收集 API 中正常進行。

對比這兩種方法：

* 媒體收集 API

   透過此即時方式，媒體播放器會在每個播放器事件上傳送追蹤資料，並每10秒傳送網路ping(每秒一秒)到後端。

* Downloaded Content API

   透過此批次處理方法，必須產生相同的工作階段事件，但儲存在裝置上，直到將它們傳送至後端作為單一作業(請參閱下方範例)。

每個方法都有其優缺點: 媒體收集 API 能即時追蹤，但需要在每個網路呼叫前進行連線檢查；Downloaded Content API 僅需要一次網路連線檢查，但也會在裝置上佔用更大的記憶體空間。

## 實施 {#section_jhp_jpk_cfb}

### 事件結構

下載的內容API是以Media Collection API為基礎，因此您的播放器批次和傳送的事件資料必須與媒體收集API中使用的事件結構相同。For information on these schemas, see: [Overview;](../media-collection-api/mc-api-overview.md) and [Validating event requests.](../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 批次裝載中的第一個事件必須為 `sessionStart`。
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. 若此參數不存在或設為 False，則 Downloaded Content API 會傳回 400 回應代碼 (Bad Request)。如此，後端就可區分下載和即時內容，並據以加以處理。(請注意，若 `media.downloaded: true` 設在即時工作階段上，則同樣會導致媒體收集 API 傳回 400 回應代碼。)

* 實施時應負責依照其外觀的順序，正確地儲存播放器事件。

### 回應代碼

* 201 - Created: Successful Request；資料有效，工作階段已建立且將進行處理。
* 400 - Bad Request；結構驗證失敗，已捨棄所有資料，不會處理任何工作階段資料。

## 與 Adobe Analytics 整合 {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. 這些是收到的第一個和最後一個事件(開始和完成)的時間戳記。此機制可讓已完成的媒體工作階段放置在正確的時間點(亦即，即使使用者未在線上返回數天，媒體會話也會回報為實際檢視內容時發生)。您必須透過建立&#x200B;*可選時間戳記報表套裝*，以在 Adobe Analytics 端啟用此機制。To enable a timestamp optional report suite, see [Timestamps Optional.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## 範例工作階段比較 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### 媒體收集 API

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

### Downloaded Content API

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

