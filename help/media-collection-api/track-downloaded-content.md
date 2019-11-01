---
title: 追蹤下載內容
description: null
uuid: 0718689d-9602-4e3f-833c-8297ae1d909
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 追蹤下載內容{#track-downloaded-content}

## 概述 {#overview}

「已下載內容」功能可讓使用者離線時追蹤媒體使用。 舉例來說，使用者在行動裝置上下載並安裝應用程式，然後使用應用程式將內容下載至裝置上的本機儲存。為追蹤此下載資料，Adobe已開發「下載內容」功能。 使用此功能，當使用者從裝置儲存空間播放內容時，追蹤資料會儲存在裝置上，而不論裝置的連線性為何。 當使用者完成播放作業，而裝置返回線上時，儲存的追蹤資訊會在單一裝載內傳送至Media Collection API後端。 在此之後，處理和報告會如常在Media Collection API中進行。

對比兩種方法：

* 線上

   使用這種即時方法，媒體播放器會在每個播放器事件上傳送追蹤資料，並且每十秒（廣告每秒）傳送網路ping，逐一傳送至後端。

* 離線（下載內容功能）

   使用此批次處理方法，需要產生相同的作業階段事件，但這些事件會儲存在裝置上，直到以單一作業階段傳送至後端（請參閱以下範例）。

每種方法都有其優缺點：
* 線上場景即時跟蹤；這需要在每次網路呼叫前先檢查連通性。
* 離線案例（「下載內容」功能）只需檢查一次網路連線，但需要在裝置上增加記憶體使用量。

## 實施 {#implementation}

### 事件結構

「下載的內容」功能只是（標準）線上Media Collection API的離線版本，因此您的播放器批次和傳送至後端的事件資料必須使用與進行線上呼叫時相同的事件結構。 有關這些方案的資訊，請參閱：
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [驗證事件要求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 批次裝載中的第一個事件必須 `sessionStart` 與平常一樣，與Media Collection API一起使用。
* **您必須在`media.downloaded: true`** 事件上加入標準中繼資料參數(`params` 索引鍵), `sessionStart` 以向後端指出您要傳送下載的內容。 如果此參數不存在或在您傳送下載的資料時設為false,API將傳回400個回應碼（錯誤請求）。 此參數可區分下載內容與後端即時內容。 (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* 實施時應負責依照其外觀的順序，正確地儲存播放器事件。

### 回應代碼

* 201 - Created: Successful Request；資料有效，工作階段已建立且將進行處理。
* 400 - Bad Request；結構驗證失敗，已捨棄所有資料，不會處理任何工作階段資料。

## 與 Adobe Analytics 整合 {#integration-with-adobe-analtyics}

在計算下載內容藍本的Analytics開始／關閉呼叫時，後端會設定一個額外的Analytics欄位，稱為 `ts.` Thees are timestamps for the first and last events received(start and complete)。 此機制可讓完成的媒體作業置於正確的時間點（即即使使用者連續數天未連線，媒體作業仍會報告在實際檢視內容時發生）。 您必須透過建立&#x200B;_可選時間戳記報表套裝，以在 Adobe Analytics 端啟用此機制。_ 若要啟用可選時間戳記報表套裝，請參閱 [可選時間戳記。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

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

