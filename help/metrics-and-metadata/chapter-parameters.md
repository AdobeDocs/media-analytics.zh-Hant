---
seo-title: 章節參數
title: 章節參數
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# 章節參數{#chapter-parameters}

本主題介紹章節與/或區段資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

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
>請勿變更下列任何變數的分類名稱，這些變數在「報告／保留變數」下描述為「分類」。\
>媒體分類是在報表套裝啟用媒體追蹤時定義的。 Adobe會不時新增屬性，當發生此情況時，客戶必須重新啟用其報表套裝，才能存取新的媒體屬性。 在更新程式中，Adobe會檢查變數的名稱，以判斷分類是否啟用。 如果其中有遺失，Adobe會再次新增遺失的。

## 章節中繼資料 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 章節名稱

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.friendlyName </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：章開始、章結 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> ****<br/> 範例值：《大爆炸2》 </li><li> **說明：**<br/>章節和／或區段的名稱。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>好記名稱) </li> <li> ****<br/> 心率：(s:stream:chapter_name) </li> </ul> | <ul> <li> **可用:**<br/>預設建立...  </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節名稱 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>好記名稱) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>好記名稱) </li> </ul> |

### 章節位置

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.index </li> <li> ****<br/> 必要：SDK:否；API:是的。 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> ****<br/> 範例值：2 </li><li> **說明：**<br/>內容中章節的位置（索引、整數）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>position) </li> <li> ****<br/> 心率：(l:stream:chapter_pos) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節位置 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>position) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>position) </li> </ul> |

### 章節位移

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.offset </li> <li> ****<br/> 必要：SDK:否；API:是的。 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> ****<br/> 範例值：58 </li><li> **說明：**<br/>內容中章節從開始到結束的偏移（以秒為單位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>偏移) </li> <li> ****<br/> 心率：(l:stream:chapter_offset) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節位移 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>偏移) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>偏移) </li> </ul> |

### 章節長度

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.chapter.length </li> <li> ****<br/> 必要：SDK:否；API:是的。 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> ****<br/> 範例值：486 </li><li> **說明：**<br/>章節的長度，以秒為單位。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>length) </li> <li> ****<br/> 心率：(l:stream:chapter_length) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節長度 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>length) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>length) </li> </ul> |

### 章節

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>自動產生的章節ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>名稱) </li> <li> ****<br/> 心率：(s:stream:chapter_id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>章節 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>名稱) </li> <li> **資料饋送:**<br/>videochapter </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>名稱) </li> </ul> |

## 章節量度 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 章節開始

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>章節開始 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>章節開始的數目。  **重要:** 若此事件已設定，則唯一可能的值為「TRUE」。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>檢視) </li> <li> ****<br/> 心率：(s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> ****<br/> 報表名稱：第g章開始 </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>檢視) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>檢視) </li> </ul> |

### 章節完成

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3</li> <li> ****<br/> 範例值：TRUE </li><li> **說明：**<br/>章節完成的數目。  **重要:** 若此事件已設定，則唯一可能的值為「TRUE」。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>complete) </li> <li> ****<br/> 心率：(s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> ****<br/> 報表名稱：章程完成g </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>complete) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>complete) </li> </ul> |

### 章節逗留時間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：章關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>在章節中的逗留時間。  該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>timePlayed) </li> <li> **心率:**<br/> </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> ****<br/> 報表名稱：章逗留時間g </li> <li> ****<br/> 上下文資料：(a.media.chapter.<br/>timePlayed) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>timePlayed) </li> </ul> |

## 相關API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
