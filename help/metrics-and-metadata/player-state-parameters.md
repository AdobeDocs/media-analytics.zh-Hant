---
title: 播放器狀態參數
description: 本主題說明播放器狀態追蹤參數。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 26%

---


# 播放器狀態參數{#player-state-parameters}

本主題提供Adobe透過解決方案變數收集的播放器狀態資料清單。

表格資料說明:

* **實作:**&#x200B;實作數值和需求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *「伴隨傳送」*- 指出資料傳送的時間:*「媒體開始」*&#x200B;為媒體開始時傳送的分析呼叫、*「廣告開始」*&#x200B;為廣告開始時傳送的分析呼叫等等；*「關閉」*&#x200B;呼叫為媒體工作階段結束或廣告、章節等項目結束時，直接從心率伺服器傳送到分析伺服器的已編譯分析呼叫。網路封包呼叫中使用無法使用關閉呼叫。
   * *最小SDK 版本* - 指出您存取參數所需的 SDK 版本。
   * *範例值* - 提供常見的變數使用方法範例。
* **網路參數：**&#x200B;顯示傳遞至 Adobe Analytics 或心率伺服器的數值。本欄顯示可於網路呼叫中看到，且由 Adobe Media SDK 產生的參數名稱。
* **報表：**&#x200B;關於如何檢視和分析視訊資料的資訊。
   * *可用* - 指出資料是否已由報表預設提供 (*是*)，或是需要自行設定 (*自訂*)
   * *保留變數* - 指出資料在保留變數中是否被當作事件、eVar、prop 或分類擷取。
   * *報表名稱* - 適用於變數的 Adobe Aanlytics 報表名稱
   * *內容資料* - 傳遞至報表伺服器以及用於處理規則的 Adobe Aanlytics 內容資料名稱。
   * *資料摘要* - 可在 Clickstream 或 Live Stream 資料摘要中找到的變數欄名稱
   * *Audience Manager* - Adobe Audience Manager 中的特徵名稱

>[!IMPORTANT]
>
>請勿變更下列任何變數的分類名稱，其說明以「分類」形式顯示於「報表/保留變數」下方。\
>為媒體追蹤啟用報表套裝時，系統會定義媒體分類。Adobe 有時會新增屬性，而發生這種情形時，客戶必須重新啟用其報表套裝才能存取新的媒體屬性。在更新程序期間，Adobe 會檢查變數名稱，藉此決定是否啟用分類。如果有任何變數名稱遺失，Adobe 會再次新增遺失的項目。

## 播放器狀態屬性 {#player-state-properties}

播放器狀態追蹤功能可附加至音訊或視訊串流。 標準化的播放器狀態追蹤度量會儲存為解決方案變數。 標準狀態為： 全螢幕、靜音、closeCaption、pictureInPicture和inFocus。

### 全螢幕屬性

#### 受全螢幕影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受全螢幕影響的串流數。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要**<br/> ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受全螢幕影響的報表名稱串流&#x200B;**<br/>,</li> <li> **內容資料&#x200B;**<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### 全螢幕次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明全螢幕的顯示次數。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，計數等於視訊處於全螢幕狀態的次數。 若此事件未設定，則不會傳送值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.count)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>「全螢幕計數」</li> <li> **內容資料&#x200B;**<br/>(media.states.fullscreen.count)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.fullscreen.count)</li> </ul> |



#### 全螢幕總時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明全螢幕的顯示時間長度。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，則時間等於視訊處於全螢幕狀態的時間。 若此事件未設定，則不會傳送值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.time)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>「全螢幕總持續時間」</li> <li> **內容資料&#x200B;**<br/>(media.states.fullscreen.time)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.fullscreen.time)</li> </ul> |


### 關閉標題屬性

#### 受隱藏式字幕影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受隱藏字幕影響的串流數。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要**<br/> ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.clousedcaptioning.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受隱藏字幕影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.cloused captioning.set)<br/> </li> <li> **Data Feed **<br/>media.states.cloused字幕</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.cloused captioning.set)</li> </ul> |


#### 隱藏式字幕次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示隱藏字幕的次數。 This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，計數等於視訊處於「隱藏字幕」狀態的次數。 若此事件未設定，則不會傳送值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>、隱藏字幕計數</li> <li> **上下文資料&#x200B;**<br/>(media.states.cloused captioning.count)<br/> </li> <li> **Data Feed **<br/>media.states.cloused captioning.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.cloused captioning.count)</li> </ul> |


#### 隱藏式字幕總時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示隱藏字幕的時間長度。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，則時間等於視訊處於「隱藏字幕」狀態的時間。 如果未設定此事件，則不會傳送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.clousedcaptioning.time)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>、隱藏字幕總持續時間</li> <li> **上下文資料&#x200B;**<br/>(media.states.closedcaptioning.time)<br/> </li> <li> **Data Feed **<br/>media.states.cloused captioning.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.cloused captioning.time)</li> </ul> |


### 靜音屬性

#### 受靜音影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明靜音影響的串流數。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要**<br/> ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **靜音影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.mute.set)<br/> </li> <li> **Data Feed **<br/>media.states.mute</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### 靜音次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明靜音的顯示次數。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，計數等於視訊處於靜音狀態的次數。 若此事件未設定，則不會傳送值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.count)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>靜音計數</li> <li> **上下文資料&#x200B;**<br/>(media.states.mute.count)<br/> </li> <li> **Data Feed **<br/>media.states.mute.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.mute.count)</li> </ul> |

#### 靜音總時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示靜音的時間長度。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，則時間等於視訊處於靜音狀態的時間。 如果未設定此事件，則不會傳送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.time)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>靜音總持續時間</li> <li> **上下文資料&#x200B;**<br/>(media.states.mute.time)<br/> </li> <li> **Data Feed **<br/>media.states.mute.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.mute.time)</li> </ul> |


### 圖片屬性中的圖片


#### 受圖片影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受圖片影響的串流數。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受圖片中圖片影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### 圖片計數中的圖片

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明「圖片」的顯示次數。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果設定此事件，計數等於視訊處於「圖片中的畫面」狀態的次數。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.count)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **圖片計數中的報表名稱&#x200B;**<br/>「圖片」</li> <li> **上下文資料&#x200B;**<br/>(media.states.pictureinpicture.count)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.pictureinpicture.count)</li> </ul> |


#### 圖片中的圖片總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「Picture in Picture（圖片中圖片）」的時間長度。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果設定此事件，則時間等於視訊處於「圖片中的畫面」狀態的時間。 如果未設定此事件，則不會傳送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.time)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **圖片總持續時間中的報表名稱圖片&#x200B;**<br/>(Report Name Picture in Picture Total Duration)</li> <li> **上下文資料&#x200B;**<br/>(media.states.pictureinpicture.time)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.pictureinpicture.time)</li> </ul> |


### 焦點屬性

#### 受觀看中影響的資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受焦點影響的串流數。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受焦點影響的報表名稱串流&#x200B;**<br/>(Report Name Streams In Focus)</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.infocus.set)<br/> </li> <li> **Data Feed **<br/>media.states.infocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### 觀看中次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「焦點」的次數。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果設定此事件，計數等於視訊處於「焦點中」狀態的次數。 若此事件未設定，則不會傳送值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.count)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **焦點計數中的報表名稱&#x200B;**<br/>(Report Name)</li> <li> **上下文資料&#x200B;**<br/>(media.states.infocus.count)<br/> </li> <li> **資料饋送&#x200B;**<br/>media.states.infocus.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.infocus.count)</li> </ul> |


#### 觀看中總時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「焦點」的時間長度。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> ：如果設定此事件，則時間等於視訊處於「焦點中」狀態的時間。 如果未設定此事件，則不會傳送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.time)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **焦點總持續時間&#x200B;**<br/>中的報表名稱</li> <li> **上下文資料&#x200B;**<br/>(media.states.infocus.time)<br/> </li> <li> **Data Feed **<br/>media.states.infocus.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.states.infocus.time)</li> </ul> |

## XDM標識的屬性清單

儲存在Analytics中的資料可用於任何用途，而「播放器狀態」量度可使用XDM匯入Adobe Experience Platform，並與「客戶歷程分析」搭配使用。

| 播放器狀態屬性 | 映射 |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## 相關 API {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
