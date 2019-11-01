---
title: 品質參數
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 品質參數{#quality-parameters}

本主題提供體驗品質 (QoE/QoS) 資料的清單，包含 Adobe 透過解決方案變數收集的內容資料值。

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

## 品質中繼資料 {#quality-metadata}

### 平均位元速率

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [位元速率](./quality-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.qoe.bitrate </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> **伴隨傳送:**<br/>關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：800-899 </li><li> **說明：**<br/>平均位元速率（以kbps為單位）。 值預先定義為 100kbps 間隔的貯體。平均位元速率的計算方式，為播放作業工作階段期間發生、與播放期間相關的所有位元速率值的加權平均。實施流量分類。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bitrateAverageBucket) </li> <li> ****<br/> 心率：(l:stream:bitrate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>平均位元速率 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bitrateAverageBucket) </li> <li> **資料摘要:**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateAverageBucket) </li> </ul> |


### 開始時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.qoe.timeToStart </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：三萬 </li><li> **說明：**<br/>如果您未透過QoSObject設定此值，此值預設為零。 您將此值設為毫秒。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>timeToStart) </li> <li> ****<br/> 心率：(l:stream:startup_time) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>開始時間 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>timeToStart) </li> <li> **資料饋送:**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>timeToStart) </li> </ul> |


### FPS

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.qoe.framesPerSecond </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：24 </li><li> **說明：**<br/>串流影格速率的目前值（每秒影格數）。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> ****<br/> 心率：(l:stream:fps) </li> </ul> | <ul> <li> **可用:**<br/>否 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>不適用 </li> <li> **上下文資料:**<br/> </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 掉格

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>droppedFrames </li> <li> **API 索引鍵:**<br/>media.qoe.droppedFrames </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：3 </li><li> **說明：**<br/>丟棄的幀數(Int)。 此值的計算方式為播放工作階段期間所有掉格的總數。此值取自(l:stream:dropped_frames)的最後一個值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>droppedFrameCount) </li> <li> ****<br/> 心率：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>掉格 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>droppedFrameCount) </li> <li> **資料饋送:**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrameCount) </li> </ul> |



### 緩衝事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：2 </li><li> **說明：**<br/>緩衝事件數。 此量度是以發生在播放作業期間的不同緩衝狀態的計數來計算。這是該播放器從其他狀態 (例如播放或暫停) 進行緩衝狀態的計數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bufferCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>緩衝事件 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bufferCount) </li> <li> **資料饋送:**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferCount) </li> </ul> |



### 總緩衝期間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** </li> <li> ****<br/> 範例值：30 </li><li> **說明：**<br/>緩衝所花費的總時間（秒）。 此值的計算方式為播放工作階段期間發生的所有緩衝事件期間的總數。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bufferTime) </li> <li> ****<br/> 心率：(l:event:duration) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>總緩衝期間 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bufferTime) </li> <li> **資料饋送:**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferTime) </li> </ul> |



### 位元速率變更

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.qoe.bitrateChange </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：3 </li><li> **說明：**<br/>位元速率變更數（整數）。 此值的計算方式為播放工作階段期間發生的所有位元速率變更事件的總數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bitrateChangeCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>位元速率變更 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bitrateChangeCount) </li> <li> **資料饋送:**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateChangeCount) </li> </ul> |



### 錯誤/錯誤事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 密鑰:**<br/> </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 </li><li> **說明：**<br/>發生的錯誤數（整數）。 此值的計算方式為播放工作階段期間發生的所有錯誤事件的總數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>errorCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>錯誤 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>errorCount) </li> <li> **資料饋送:**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>errorCount) </li> </ul> |



### 播放器 SDK 錯誤 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>播放器SDK產生的唯一錯誤ID。 客戶必須透過系統提供的錯誤 API，在實施時提供錯誤代碼/ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>playerSdkErrors) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>錯誤 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>playerSdkErrors) </li> <li> ****<br/> 資料饋送：videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>playerSdkErrors) </li> </ul> |



### 外部錯誤 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>任何外部來源的唯一錯誤ID，例如CDN錯誤。 客戶必須透過系統提供的錯誤 API，在實施時提供錯誤代碼/ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>externalErrors) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>錯誤 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>externalErrors) </li> <li> ****<br/> 資料饋送：videoqoeexteneralerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>externalErrors) </li> </ul> |



### Media SDK 錯誤 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>Media SDK在播放期間產生的唯一錯誤ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>mediaSdkErrors) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>錯誤 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>mediaSdkErrors) </li> <li> **資料饋送:** <br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>mediaSdkErrors) </li> </ul> |




### 作業結束 {#session-end}

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 2.1 </li> <li> ****<br/> 範例值：end </li><li> **說明：**<br/>結束事件表示SDK正在向後端傳送關閉呼叫。 接收此事件後，後端會關閉此影片的作業階段，不會進行後續處理。<br/>如果媒體完成為100%，則應在查看內容完成後傳 `s:event:type=complete.` 送 [此內容](audio-video-parameters.md#content-complete) ，以取得相關資訊。 </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> ****<br/> 心率：(s:event:type=end) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>不適用 </li> <li> **上下文資料:**<br/> </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager:**<br/> </li> </ul> |



## 品質量度 {#quality-metrics}

### 開始時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：三萬 </li><li> **說明：**<br/>如果您未透過QoSObject設定此值，此值預設為零。 您將此值設為毫秒。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>timeToStart) </li> <li> ****<br/> 心率：(l:stream:startup_time) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>開始時間 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>timeToStart) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>timeToStart) </li> </ul> |



### 緩衝事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：2 </li><li> **說明：**<br/>緩衝事件數（整數）。 此度量的計算方式為播放工作階段期間發生的緩衝事件的計數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bufferCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>緩衝事件 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bufferCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferCount) </li> </ul> |



### 總緩衝期間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：15 </li><li> **說明：**<br/>緩衝的總逗留時間(秒；整數)。 此值的計算方式為播放工作階段期間發生的所有緩衝事件期間的總數。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bufferTime) </li> <li> ****<br/> 心率：(l:event:duration) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>總緩衝期間 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bufferTime) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferTime) </li> </ul> |



### 位元速率變更

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>事件 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值："3" </li><li> **說明：**<br/>位元速率變更的數目。 此值的計算方式為播放工作階段期間發生的所有位元速率變更事件的總數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>bitrateChangeCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>位元速率變更 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>bitrateChangeCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateChangeCount) </li> </ul> |



### 錯誤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 </li><li> **說明：**<br/>發生的錯誤數（整數）。 此值的計算方式為播放工作階段期間發生的所有錯誤事件的總數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>errorCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>錯誤事件 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>errorCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>errorCount) </li> </ul> |



### 掉格

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 </li><li> **說明：**<br/>捨棄的影格數（整數）。 此值的計算方式為播放工作階段期間所有掉格的總數。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>droppedFrameCount) </li> <li> ****<br/> 心率：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>掉格 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>droppedFrameCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrameCount) </li> </ul> |



### 開始前掉格

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>使用者在視訊開始前結束視訊的次數。 只有在未轉譯任何內容 (不論是否為廣告) 時，此度量才會設為 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>dropBeforeStart) </li> <li> ****<br/> 心率：(s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>開始前掉格 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>dropBeforeStart) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 緩衝影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>受緩衝影響的串流數。 只有在播放工作階段期間發生至少一個緩衝事件時，此度量才會設為 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>buffer) </li> <li> ****<br/> 心率：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>緩衝影響的資料流量 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>buffer) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 位元速率變更影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>位元速率變更的串流數。 只有在播放工作階段期間發生至少一個位元速率變更事件時，此度量才會設為 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>位元速率變更) </li> <li> ****<br/> 心率：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> ****<br/> 報表名稱：位元速率變更影響的串流 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>位元速率變更) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>位元速率變更) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 平均位元速率

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：3200 </li><li> **說明：**<br/>平均位元速率（以kbps、整數為單位）。 此度量的計算方式為播放工作階段期間發生、與播放期間相關的所有位元速率值的平均比重。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>位元速率平均值) </li> <li> ****<br/> 心率：(l:stream:bitrate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>平均位元速率 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>位元速率平均值) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>位元速率平均值) </li> </ul> |



### 錯誤影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>發生錯誤事件的串流數(即在播放作業階段期間 `trackError` 呼叫，並產生心 `type=error` 率呼叫)。 </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>error) </li> <li> ****<br/> 心率：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>錯誤影響的資料流量 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>error) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>error) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 掉格影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>放置幀的流數。 只有在播放工作階段期間發生至少一個掉格時，此度量才會設為 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>droppedFrames) </li> <li> ****<br/> 心率：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>掉格影響的資料流量 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>droppedFrames) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 停頓影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5+ </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>發生停頓事件的串流數。 只有在播放時發生了至少一次停頓，此量度才會設定為 1。客戶必須建立自己的處理規則，才能有可用於報表的值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>stall) </li> <li> ****<br/> 心率：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>事件 </li> <li> **報告名稱:**<br/> </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>stall) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stall) </li> </ul> |



>[!IMPORTANT]
>如果設定此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。

### 停頓事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5+ </li> <li> ****<br/> 範例值："3" </li><li> **說明：**<br/>播放作業期間停止播放的次數。 客戶必須建立自己的處理規則，才能有可用於報表的值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>stallCount) </li> <li> ****<br/> 心率：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>事件 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>stallCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stallCount) </li> </ul> |



### 總停頓期間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5+ </li> <li> ****<br/> 範例值：12 </li><li> **說明：**<br/>總時間(秒；整數)播放在播放工作階段期間停止。 客戶必須建立自己的處理規則，才能有可用於報表的值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe)。<br/>stallTime) </li> <li> ****<br/> 心率：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>事件 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.qoe)。<br/>stallTime) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stallTime) </li> </ul> |



## 相關API {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

