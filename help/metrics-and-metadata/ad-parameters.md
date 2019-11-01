---
title: 廣告參數
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 廣告參數{#ad-parameters}

本主題介紹視訊廣告資料，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作:**&#x200B;實作數值和要求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *傳送方式* -指出資料的傳送時間：媒 *體開始* (Media Start)是媒體開始時傳送的分析呼叫， *廣告開始(* Ad Start)是廣告開始時傳送的分析呼叫，等等；關閉呼 *叫* ，是指在媒體作業階段結束時或廣告結束時，從心率伺服器直接傳送至分析伺服器的編譯分析呼叫。 關閉呼叫在網路資料包呼叫中不可用。
   * *最小 SDK 版本* - 指出您存取參數所需的 SDK 版本。
   * *範例值* - 提供常見的變數使用方法範例。
* **網路參數:**&#x200B;顯示傳遞至 Adobe Analytics 或心率伺服器的數值。本欄顯示可於網路呼叫中看到，且由 Adobe Media SDK 產生的參數名稱。
* **報表:**&#x200B;關於如何檢視和分析視訊資料的資訊。
   * *可用* - 指出資料是否已由報表預設提供 (*是*)，或是需要自行設定 (*自訂*)
   * *預留變數* - 指出資料在預留變數中是否被當作事件、eVar、prop 或分類擷取。
   * *報表名稱* - 適用於變數的 Adobe Aanlytics 報表名稱
   * *內容資料* - 傳遞至報表伺服器以及用於處理規則的 Adobe Aanlytics 內容資料名稱。
   * *資料饋送* - 可在 Clickstream 或 Live Stream 資料饋送中找到的變數欄位名稱
   * *Audience Manager* - Adobe Audience Manager 中的特徵名稱

>[!IMPORTANT]
>
>請勿變更下列任何變數的分類名稱：
>在「報告／保留變數」下描述為「分類」。
>媒體分類是在報表套裝啟用媒體時定義的
>追蹤. Adobe會不時新增屬性，當發生此情況時，
>客戶必須重新啟用其報表套裝，才能存取新媒體
>屬性。 在更新程式期間，Adobe會判斷
>可透過檢查變數名稱來啟用分類。 如果有任何
>遺失，Adobe會再次新增遺失的。

## 廣告視訊資料 {#ad-video-data}

### 廣告 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.id </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本  </li> <li> ****<br/> 範例值：《2125》 </li><li> **說明：**<br/>廣告的ID。 (任何整數和/或字母的組合)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>名稱) </li> <li> ****<br/> 心率：(s:asset:ad_id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>廣告 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>名稱) </li> <li> **資料饋送:**<br/>videoad </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Pod 位置中的廣告

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.podPosition </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 </li><li> **說明：**<br/>廣告在父廣告插播內的位置（索引）。 第一個廣告索引為 0，第二個廣告索引為 1，以此類推。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>podPosition) </li> <li> ****<br/> 心率：(s:asset:pod_position) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>Pod 位置中的廣告 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>podPosition) </li> <li> **資料饋送:**<br/>videoadinpod </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 廣告長度

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.length </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> ****<br/> 範例值："15"  </li><li> **說明：**<br/>視訊廣告的長度（秒）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>length) </li> <li> ****<br/> 心率：(l:asset:ad_length) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar 和分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>廣告長度和廣告長度 (變數) </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>length) </li> <li> **資料饋送:**<br/>videoadlength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### 廣告播放器名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.playerName </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值："自由輪" </li><li> **說明：**<br/>負責轉譯廣告的播放器名稱。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>playerName) </li> <li> ****<br/> 心率：(s:sp:player_name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>廣告播放器名稱 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>playerName) </li> <li> **資料饋送:**<br/>videoadplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 廣告插播名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.podFriendlyName </li> <li> ****<br/> 必要：SDK:是的；API:不。 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值："前滾" </li><li> **說明：**<br/>廣告插播的好記名稱。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>podFriendlyName) </li> <li> ****<br/> 心率：(s:asset:pod_name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>Pod 名稱 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>podFriendlyName) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 廣告插播索引

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.podPosition </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **伴隨傳送:**<br/> </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 </li><li> **說明：**<br/>內容中廣告分段的索引，從1開始。 此屬性&#x200B;**僅**&#x200B;由 Media SDK 用於產生 Pod ID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **心率:**<br/> </li> </ul> | <ul> <li> **可用:**<br/>否 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>不適用 </li> <li> **上下文資料:**<br/> </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 廣告插播位置

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.podSecond </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：90 </li><li> **說明：**<br/>內容中廣告分段的偏移（以秒為單位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>podSecond) </li> <li> ****<br/> 心率：(l:asset:pod_offset) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>Pod 位置 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>podSecond) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 廣告插播 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>pod) </li> <li> ****<br/> 心率：(s:asset:pod_id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>廣告 Pod </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>pod) </li> <li> **資料饋送:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 廣告名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./ad-parameters.md#section_Related_APIs) </li> <li> **API 索引鍵:**<br/>media.ad.name </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> ****<br/> 範例值："福特F-150" </li><li> **說明：**<br/>廣告的好記名稱。  在報表中，「廣告名稱」為分類，而「廣告名稱 (變數)」為 eVar。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>好記名稱) </li> <li> ****<br/> 心率：(s:asset:ad_name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar 和分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>廣告名稱和廣告名稱 (變數) </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>好記名稱) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 標準廣告中繼資料 {#standard-ad-metadata}

### 廣告商

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>ADVERTISER </li> <li> **API 索引鍵:**<br/>media.ad.advertiser </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>廣告中包含產品的公司／品牌。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>advertiser) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i>廣告商 </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>advertiser) </li> <li> **資料饋送:**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### 行銷活動 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>CAMPAIGN_ID </li> <li> **API 索引鍵:**<br/>media.ad.campaignId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：整數或名稱（字串）。  </li><li> **說明：**<br/>廣告促銷活動的ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>campaign) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i>行銷活動 ID </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>campaign) </li> <li> **資料饋送:**<br/>videocampaign </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### 創作 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>CREATIVE_ID </li> <li> **API 索引鍵:**<br/>media.ad.creativeId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：整數或名稱（字串）。  </li><li> **說明：**<br/>廣告創意素材的ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>創意) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i>創作 ID </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>創意) </li> <li> **資料饋送:**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### 網站 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SITE_ID </li> <li> **API 索引鍵:**<br/>media.ad.siteId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>廣告網站的ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>網站) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自訂處理規則 </i> </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i> </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>網站) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### 創作 URL

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>CREATIVE_URL </li> <li> **API 索引鍵:**<br/>media.ad.creativeURL </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>廣告創意素材的URL。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>creativeURL) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自訂處理規則 </i> </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i> </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>creativeURL) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### 版面 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>PLACEMENT_ID </li> <li> **API 索引鍵:**<br/>media.ad.placementId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始、廣告關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>廣告的位置ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>位置) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自訂處理規則 </i> </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> <i> </i> </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>位置) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 廣告量度 {#ad-metrics}

### 廣告開始

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告開始 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>視訊廣告開始數。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>檢視) </li> <li> ****<br/> 心率： (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>廣告開始 </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>檢視) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### 廣告完成

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>視訊廣告完成數。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>complete) </li> <li> ****<br/> 心率：(s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>廣告完成 </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>complete) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 廣告逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>廣告關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：15 </li><li> **說明：**<br/>觀看廣告所花費的總時間（以秒為單位）（即播放的秒數）。  該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad。<br/>timePlayed) </li> <li> **心率:**<br/> </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>廣告逗留時間 </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> 上下文資料：(a.media.ad。<br/>timePlayed) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## 相關API {#section_Related_APIs}

### createAdObject API:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

