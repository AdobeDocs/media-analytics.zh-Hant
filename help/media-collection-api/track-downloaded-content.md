---
title: 追蹤下載內容
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 56%

---


# 追蹤下載內容{#track-downloaded-content}

## 概述 {#overview}

「下載內容」功能提供可在使用者離線時追蹤媒體消耗的功能。例如，使用者下載應用程式並在行動裝置上安裝應用程式，然後使用應用程式將內容下載至裝置上的本機儲存。 為追蹤下載的資料，Adobe開發了「下載內容」功能。 使用此功能，當使用者從裝置儲存空間播放內容時，追蹤資料會儲存在裝置上，而不論裝置的連線性為何。 當使用者完成播放工作階段，而裝置返回線上時，儲存的追蹤資訊會傳送至單一裝載內的Media Collection API後端。 儲存的追蹤資訊會照常在媒體收集API中處理和報告。

對照下列兩種方法:

* 線上

   使用這種即時方法，媒體播放器會傳送每個播放器事件的追蹤資料，並且每十秒（廣告每秒）傳送網路ping，逐一傳送至後端。

* 離線 (「下載內容」功能)

   使用此批次處理方法，需要產生相同的作業事件，但這些事件會儲存在裝置上，直到以單一作業傳送至後端（請參閱以下範例）。

每種方法都有各自的優缺點:
* 線上情況可進行即時追蹤，但需要在每個網路呼叫前進行連線檢查。
* 離線情況 (「下載內容」功能) 僅需要一次網路連線檢查，但也會在裝置上佔用更大的記憶體空間。

## 實施 {#implementation}

### 支援的平台

iOS和Android行動裝置支援內容追蹤。

### 事件結構

「下載內容」功能是（標準）線上Media Collection API的離線版本，因此您的播放器批次和傳送至後端的事件資料必須使用與進行線上呼叫時相同的事件結構。 如需這些結構的詳細資訊，請參閱:
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 根據 Media Collection API 通常的情況，批次裝載中的第一個事件必須為 `sessionStart`。
* 在 **事件上，`media.downloaded: true`**您必須將`params`包含在標準中繼資料參數 (`sessionStart`索引鍵) 中，以表示您要將下載內容傳送到哪個後端。若此參數不存在或設為 false，在傳送下載資料時，API 會傳回 400 回應代碼 (Bad Request)。此參數會區分傳送到後端的下載內容與即時內容If`media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the API.
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

## 媒體追蹤器API參考

如需如何設定下載內容的詳細資訊，請參閱媒 [體追蹤器API參考](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference)。
