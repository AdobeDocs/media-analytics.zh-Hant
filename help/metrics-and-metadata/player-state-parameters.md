---
title: 播放器狀態參數
description: 本主題說明播放器狀態追蹤參數。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

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

「播放器狀態追蹤」屬性表格會依下列五個區段組織：

* 全螢幕
   * 受全螢幕影響的串流
   * 全螢幕計數
   * 全螢幕總持續時間
* 關閉標題
   * 受隱藏字幕影響的串流
   * 隱藏字幕計數
   * 隱藏字幕的總持續時間
* 靜音
   * 靜音影響的串流
   * 靜音計數
   * 靜音總持續時間
* 畫中畫
   * 受圖片影響的串流
   * 圖片計數中的圖片
   * 圖片中的圖片總持續時間
* 焦點
   * 受焦點影響的串流
   * 焦點計數
   * 焦點總持續時間

### 全螢幕屬性

#### 受全螢幕影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受全螢幕影響的串流數。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受全螢幕影響的報表名稱串流&#x200B;**<br/>,</li> <li> **內容資料&#x200B;**<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostatefullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### 全螢幕計數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明全螢幕的顯示次數。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>「全螢幕計數」</li> <li> **上下文資料&#x200B;**<br/>(videostatefullscreencount)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostatefullscreencount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreencount)</li> </ul> |



#### 全螢幕總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明全螢幕的顯示時間長度。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreentime)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>「全螢幕持續時間」</li> <li> **上下文資料&#x200B;**<br/>(videostatefullscreentime)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostatefullscreentime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreentime)</li> </ul> |


### 關閉標題屬性

#### 受隱藏字幕影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受隱藏字幕影響的串流數。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.clousedcaptioning.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受隱藏字幕影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.cloused captioning.set)<br/> </li> <li> **Data Feed **<br/>videostateclosed字幕</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.cloused captioning.set)</li> </ul> |


#### 隱藏字幕計數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明選取隱藏字幕的次數。 This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>、隱藏字幕計數</li> <li> **上下文資料&#x200B;**<br/>(videostateclosedcaptioningcount)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostateclosedcaptioningcount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioncount)</li> </ul> |


#### 隱藏字幕的總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明選取「隱藏字幕」的時間長度。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>、隱藏字幕持續時間</li> <li> **上下文資料&#x200B;**<br/>(videostateclosedcaptioningtime)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostateclosedcaptioningtime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptiontime)</li> </ul> |


### 靜音屬性

#### 靜音影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明靜音影響的串流數。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **靜音影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.mute.set)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostatement</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### 靜音計數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明選取靜音的次數。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemecount)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>靜音計數</li> <li> **上下文資料&#x200B;**<br/>(videostatemoutecount)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostatecount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatecount)</li> </ul> |

#### 靜音總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明選取「靜音」的時間長度。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemetime)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **報表名稱&#x200B;**<br/>靜音持續時間</li> <li> **上下文資料&#x200B;**<br/>(videostatesuitetime)<br/> </li> <li> **Data Feed **<br/>videostatetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemetime)</li> </ul> |


### 圖片屬性中的圖片


#### 受圖片影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受圖片影響的串流數。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受圖片中圖片影響的報表名稱串流&#x200B;**<br/>（英文）</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicture</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### 圖片計數中的圖片

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明「圖片」的顯示次數。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturescount)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **圖片計數中的報表名稱&#x200B;**<br/>「圖片」</li> <li> **上下文資料&#x200B;**<br/>(videostatepictureinpicturescounti)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicturescount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatepictureinpicturescountile)</li> </ul> |


#### 圖片中的圖片總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「Picture in Picture（圖片中圖片）」的時間長度。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **圖片持續時間中的報表名稱&#x200B;**<br/>（圖片長度）圖片</li> <li> **上下文資料&#x200B;**<br/>(videostatepictureinpicturetime)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicturetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### 焦點屬性

#### 受焦點影響的串流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明受焦點影響的串流數。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **受焦點影響的報表名稱串流&#x200B;**<br/>(Report Name Streams In Focus)</li> <li> **上下文資料&#x200B;**<br/>(a.media.states.infocus.set)<br/> </li> <li> **Data Feed **<br/>videostateinfocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### 焦點計數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「焦點」的次數。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **焦點計數中的報表名稱&#x200B;**<br/>(Report Name)</li> <li> **上下文資料&#x200B;**<br/>(videostateinfocuscount)<br/> </li> <li> **資料饋送&#x200B;**<br/>videostateinfocuscount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocuscount)</li> </ul> |


#### 焦點總持續時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK金鑰&#x200B;**<br/>（自動設定）</li> <li> **API金鑰&#x200B;**<br/>N/A</li> <li> **必要&#x200B;**<br/>否</li> <li> **類型&#x200B;**<br/>號</li> <li> **隨媒體關閉&#x200B;**<br/>(Media Close)傳送</li> <li> **最小SDK Version **<br/>3.0</li> <li> **範例值&#x200B;**<br/>TRUE</li><li> **說&#x200B;**<br/>明顯示「焦點」的時間長度。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果設定了此事件，則唯一可能的值為TRUE。 若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **心率&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>是</li> <li> **保留變數&#x200B;**<br/>事件</li> <li> **焦點持續時間中的報表名稱&#x200B;**<br/>(Report Name In Focus Duration)</li> <li> **上下文資料&#x200B;**<br/>(videostateinfocustime)<br/> </li> <li> **Data Feed **<br/>videostateinfocustime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocustime)</li> </ul> |



## 相關 API {#related_apis_section}

需要： 新增API連結至檔案：
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
