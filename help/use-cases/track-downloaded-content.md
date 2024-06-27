---
title: 如何在串流媒體收集附加元件中追蹤離線下載的內容
description: 了解如何使用「下載內容」功能在使用者離線時追蹤媒體用量。
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 98%

---

# 追蹤下載內容{#track-downloaded-content}

## 概觀 {#overview}

「下載內容」功能可供使用者在離線時追蹤媒體用量。例如，使用者可在行動裝置上下載及安裝應用程式，接著使用應用程式將內容下載至裝置上的本機儲存空間。 Adobe 特地開發「下載內容」功能，以便使用者追蹤其下載的資料。透過此功能，使用者從裝置的儲存空間播放內容時，無論裝置是否連線，追蹤資料都會儲存在裝置上。使用者完成播放工作階段，且裝置恢復成上線狀態時，儲存的追蹤資訊會隨即傳送至單一裝載中的 Media Collection API 後端。之後，儲存的追蹤資訊會照常在 Media Collection API 中處理及製成報告。

對比下列兩種方法：

* 線上

  透過這種即時處理法，媒體播放器會傳送每個播放器事件的追蹤資料，且每十秒傳送一次網路 Ping (廣告則是每秒傳送)，將資料依序傳送至後端。

* 離線 (「下載內容」功能)

  透過這種批次處理法，系統需產生相同的工作階段事件，不過會暫時將其儲存在裝置上，直到資料以單一工作階段形式傳送到後端為止 (請參閱下方範例)。

兩種方法各有優缺點：
* 線上情況有利於即時追蹤，但需在每個網路呼叫前檢查連線。
* 離線情況 (「下載內容」功能) 僅需檢查一次網路連線，但會佔用裝置上更大的記憶體空間。

## 實施 {#implementation}

### 支援平台

iOS 和 Android 行動裝置均支援內容追蹤功能。

### 事件結構

「下載內容」功能是離線版本的 (標準) 線上 Media Collection API，因此播放器批次處理及傳送到後端的事件資料，必須使用與線上呼叫時相同的事件結構。如需這些結構的詳細資訊，請參閱：
* [概觀;](/help/implementation/media-collection-api/mc-api-overview.md)
* [驗證事件請求](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件順序

* 根據 Media Collection API 通常的情況，批次裝載中的第一個事件必須為 `sessionStart`。
* 在 **事件上，`media.downloaded: true`**&#x200B;您必須將 `params` 包含在標準中繼資料參數 (`sessionStart` 索引鍵) 中，以表示您要將下載內容傳送到哪個後端。若此參數不存在或設為 false，在傳送下載資料時，API 會傳回 400 回應代碼 (Bad Request)。此參數會區分傳送到後端的下載內容與即時內容。若 `media.downloaded: true` 設在即時工作階段上，同樣會導致 API 傳回 400 回應代碼。
* 實施時應負責依照其外觀的順序，正確地儲存播放器事件。

### 回應代碼

* 201 - Created：成功的請求；資料有效，工作階段已建立且將進行處理。
* 400 - Bad Request；結構驗證失敗，已捨棄所有資料，不會處理任何工作階段資料。

## 與 Adobe Analytics 整合 {#integration-with-adobe-analtyics}

計算下載內容情況的 Analytics 開啟/關閉呼叫時，後端會設定一個稱為 `ts.` 的額外 Analytics 欄位。這些是第一個和最後一個收到事件的時間戳記 (開始和完成)。此機制可將完成的媒體工作階段放置在正確的時間點 (換句話說，即使使用者數天未重新上線，媒體工作階段也會依照實際檢視內容的時間，回報媒體工作階段)。您必須透過建立&#x200B;_可選時間戳記報表套裝，以在 Adobe Analytics 端啟用此機制。_&#x200B;若要啟用可選時間戳記報表套裝，請參閱[可選時間戳記](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=zh-Hant)。

## 範例工作階段比較 {#sample-session-comparison}

### 線上內容

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### 淘汰通知

>[!IMPORTANT]
>
>下載內容先前也可以傳送到`/api/v1/sessions`API。這種追蹤下載內容的方式&#x200B;**已過時**&#x200B;並且未來將&#x200B;**移除**。


`/api/v1/sessions` API 將只接受工作階段初始化事件。
使用新的 API 時，之前的強制性 `media.downloaded`標幟不再是必要的。
我們強烈建議使用 `/api/v1/downloaded` API 進行新下載內容實施，以及更新依賴舊 API 的現有實施。


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## 媒體追蹤器 API 參考

如需如何設定下載內容的詳細資訊，請參閱[媒體追蹤器 API 參考](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)。
