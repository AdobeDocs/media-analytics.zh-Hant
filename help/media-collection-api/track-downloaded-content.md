---
title: 追蹤下載內容
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 追蹤下載內容{#track-downloaded-content}

## 概述 {#overview}

「下載內容」功能提供可在使用者離線時追蹤媒體消耗的功能。舉例來說，使用者在行動裝置上下載並安裝應用程式，然後使用應用程式將內容下載至裝置上的本機存放區。Adobe 已開發「下載內容」功能以追蹤此下載資料。透過此功能，當使用者從裝置的儲存播放內容時，無論裝置是否連線，追蹤資料都會儲存在裝置上。當使用者完成播放工作階段且裝置回到上線狀態時，儲存的追蹤資訊會傳送至單一裝載中的媒體收集 API 後端。從該位置，處理和報表程序會在 Media Collection API 中正常進行。

對照下列兩種方法:

* 線上

   透過此即時方法，媒體播放器會傳送每個播放器事件的追蹤資料，且每十秒傳送一次網路 Ping (廣告則是每一秒)，依序傳送至後端。

* 離線 (「下載內容」功能)

   透過此批次處理方法，需要產生相同的工作階段事件，且將其儲存在裝置上，直到以單一工作階段形式將其傳送到後端為止 (請參閱下方範例)。

每種方法都有各自的優缺點:
* 線上情況可進行即時追蹤，但需要在每個網路呼叫前進行連線檢查。
* 離線情況 (「下載內容」功能) 僅需要一次網路連線檢查，但也會在裝置上佔用更大的記憶體空間。

## 實施 {#implementation}

### 事件結構

「下載內容」功能只是離線版本的 (標準) 線上 Media Collection API，因此播放器批次處理和傳送到後端的事件資料，必須使用與進行線上呼叫時相同的事件結構。如需這些結構的詳細資訊，請參閱:
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 根據 Media Collection API 通常的情況，批次裝載中的第一個事件必須為 `sessionStart`。
* 在 **事件上，`media.downloaded: true`**您必須將`params`包含在標準中繼資料參數 (`sessionStart`索引鍵) 中，以表示您要將下載內容傳送到哪個後端。若此參數不存在或設為 false，在傳送下載資料時，API 會傳回 400 回應代碼 (Bad Request)。此參數會區分傳送到後端的下載內容與即時內容(請注意，若`media.downloaded: true`設在即時工作階段上，則同樣會導致 API 傳回 400 回應代碼)。
* 實施時應負責依照其外觀的順序，正確地儲存播放器事件。

### 回應代碼

* 201 - Created：成功的要求；資料有效，工作階段已建立且將進行處理。
* 400 - Bad Request；結構驗證失敗，已捨棄所有資料，不會處理任何工作階段資料。

## 與 Adobe Analytics 整合 {#integration-with-adobe-analtyics}

計算下載內容情況的 Analytics 開啟/關閉呼叫時，後端會設定一個稱為 `ts.` 的額外 Analytics 欄位。這些是第一個和最後一個收到事件的時間戳記 (開始和完成)。此機制可將完成的媒體工作階段放置在正確的時間點 (換句話說，即使使用者數天未重新上線，媒體工作階段也會依照實際檢視內容的時間，回報媒體工作階段)。您必須透過建立&#x200B;_可選時間戳記報表套裝，以在 Adobe Analytics 端啟用此機制。_&#x200B;若要啟用可選時間戳記報表套裝，請參閱[可選時間戳記](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/timestamp-optional.html)。

## 範例工作階段比較 {#sample-session-comparison}

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

### 下載內容

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

