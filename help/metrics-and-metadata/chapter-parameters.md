---
title: 章節參數
description: 「了解有關實作、網路和報表的章節參數。」
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 01afcf648f13af4d47b5fb41b7c9e89c2a89f590
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 91%

---

# 章節參數{#chapter-parameters}

本主題介紹章節與/或區段資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作：**&#x200B;實作數值和需求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本影片追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *「伴隨傳送」*- 指出資料傳送的時間:*「媒體開始」*&#x200B;為媒體開始時傳送的分析呼叫、*「廣告開始」*&#x200B;為廣告開始時傳送的分析呼叫等等；*「關閉」*&#x200B;呼叫為媒體工作階段結束或廣告、章節等項目結束時，直接從心率伺服器傳送到分析伺服器的已編譯分析呼叫。網路封包呼叫中使用無法使用關閉呼叫。
   * *最低SDK 版本* - 指出您存取參數所需的 SDK 版本。
   * *樣本值* - 提供常見的變數使用方法範例。
* **網路參數：**&#x200B;顯示傳遞至 Adobe Analytics 或心率伺服器的數值。本欄顯示可於網路呼叫中看到，且由 Adobe Media SDK 產生的參數名稱。
* **報表：**&#x200B;關於如何檢視和分析影片資料的資訊。
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

## 章節中繼資料 {#chapter-metadata}

### 章節名稱

|   實施   | 網路參數 | 報表 |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/> media.chapter.friendlyName </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 章節開始、章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值:**<br/>「The Big Bang Chapter 2 - Dating」 </li><li> **說明:**<br/>&#x200B;章節和/或區段名稱。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **心率:**<br/>(s:stream:chapter_name) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;預設建立...  </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;章節名稱 </li> <li> **內容資料:**<br/> (a.media.chapter.<br/>友好名稱) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>友好名稱) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>chapterAssetReference.dc:title </li> <li> **集合XDM欄位路徑：**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### 章節位置

|   實施   | 網路參數 | 報表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/> media.chapter.index </li> <li> **必要:**<br/> SDK: 否；API: 是。 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值：**<br/> 2 </li><li> **說明:**<br/>&#x200B;內容內的章節位置 (索引、整數)。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>position) </li> <li> **心率:**<br/>(l:stream:chapter_pos) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;章節位置 </li> <li> **內容資料:**<br/> (a.media.chapter.<br/>位置) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>位置) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>第AssetViewDetails.index章 </li> <li> **集合XDM欄位路徑：**<br/> mediaCollection.chapterDetails.index </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### 章節位移

|   實施   | 網路參數 | 報表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/> media.chapter.offset </li> <li> **必要:**<br/> SDK: 否；API: 是。 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值：**<br/> 58 </li><li> **說明:**<br/>&#x200B;內容內從頭開始的章節位移 (以秒為單位)。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>offset) </li> <li> **心率:**<br/>(l:stream:chapter_offset) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;章節位移 </li> <li> **內容資料:**<br/> (a.media.chapter.<br/>偏移) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>偏移) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>chapterAssetViewDetails.offset </li> <li> **集合XDM欄位路徑：**<br/> mediaCollection.chapterDetails.offset </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### 章節長度

|   實施   | 網路參數 | 報表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.chapter.length </li> <li> **必要:**<br/> SDK: 否；API: 是。 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值：**<br/> 486 </li><li> **說明:**<br/>&#x200B;章節長度 (以秒為單位)。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>length) </li> <li> **心率:**<br/>(l:stream:chapter_length) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;章節長度 </li> <li> **內容資料:**<br/> (a.media.chapter.<br/>長度) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>長度) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>chapterAssetReference.xmpDM:duration </li> <li> **集合XDM欄位路徑：**<br/> mediaCollection.chapterDetails.length </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### 章節

|   實施   | 網路參數 | 報表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值：**<br/> </li><li> **說明:**<br/>&#x200B;自動產生的章節唯一 ID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>名稱) </li> <li> **心率:**<br/>(s:stream:chapter_id) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;章節 </li> <li> **內容資料:**<br/> (a.media.chapter.<br/>名稱) </li> <li> **資料摘要:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>名稱) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>章AssetReference。@id </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.chapterID </li> </ul> |

## 章節量度 {#chapter-Metrics}

### 章節開始

|   實施   | 網路參數 | 報表 |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定  </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/>&#x200B;章節開始 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值:**<br/> TRUE </li><li> **說明:**<br/>&#x200B;章節開始的數量。**重要:** 若此事件已設定，則唯一可能的值為 TRUE。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>檢視) </li> <li> **心率:**<br/>(s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;章節開始</li> <li> **內容資料:**<br/> (a.media.chapter.<br/>檢視) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>檢視) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.chapterCount。<br/>值> 0 => &quot;TRUE&quot; </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### 章節完成

|   實施   | 網路參數 | 報表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定  </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3</li> <li> **樣本值:**<br/> TRUE </li><li> **說明:**<br/>&#x200B;章節完成的數量。**重要:** 若此事件已設定，則唯一可能的值為 TRUE。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>complete) </li> <li> **心率:**<br/>(s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;章節完成</li> <li> **內容資料:**<br/> (a.media.chapter.<br/>完成) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>完成) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>comples.value </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### 章節逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定  </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 章節關閉 </li> <li> **最小SDK 版本:** 1.3 </li> <li> **樣本值：**<br/> </li><li> **說明:**<br/>&#x200B;在章節逗留的時間。該值將在 Analysis Workspace 和 Reports &amp; Analytics 中以時間格式 (HH:MM:SS) 顯示。 在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter)<br/>timePlayed) </li> <li> **心率:**<br/> </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;章節逗留時間</li> <li> **內容資料:**<br/> (a.media.chapter.<br/>播放時間) </li> <li> **資料摘要:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata)。<br/>a.media.chapter。<br/>播放時間) </li> <li> **XDM欄位路徑：**<br/> media.mediaTimed.mediaChapter。<br/>timePlayed.value </li> <li> **報告XDM欄位路徑：**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## 相關 API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:長度:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
