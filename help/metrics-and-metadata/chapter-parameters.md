---
seo-title: 章節參數
title: 章節參數
uuid: 2a6b9247-a694-46e9-98e1-424c08 c27 ec2
translation-type: tm+mt
source-git-commit: f7ffb9a88f1cf3ffefba0ae5508a857fa3de8432

---


# 章節參數{#chapter-parameters}

本主題介紹章節與/或區段資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作:**&#x200B;實作數值和要求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *隨附於* -表示傳送資料時： *媒體開始* 是在媒體開始時傳送的分析呼叫， *廣告開始* 是在廣告開始時傳送的分析呼叫等等； *關閉* 呼叫是直接從心率伺服器傳送至媒體工作階段結束處的編譯分析呼叫，或是廣告、章節等結尾的編譯分析呼叫。網路封包呼叫無法使用關閉呼叫。
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
>請勿變更以下任何列於「報告/保留變數」下方的變數分類名稱，作為「分類」。\
>媒體分類是在報告套裝啓用媒體追蹤時定義。Adobe會不時新增屬性，當發生這種情況時，客戶必須重新啓用報表套裝，才能存取新媒體屬性。在更新過程中，Adobe會檢查變數名稱，判斷分類是否啓用。如果其中有任何項目遺失，Adobe會再次新增遺漏的項目。

## 章節中繼資料 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 章節名稱

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.friendlyName </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 章節開始，章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> 「The Big Bang第章- Dashing」 </li><li> **說明：**<br/>章節及/或區段的名稱。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>friendlyName) </li> <li> **心率：**<br/> (s：串流：preview_ name) </li> </ul> | <ul> <li> **可用:**<br/>預設建立...  </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節名稱 </li> <li> **上下文資料：**<br/> (a. media. page。<br/>friendlyName) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>friendlyName) </li> </ul> |

### 章節位置

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.index </li> <li> **需要：**<br/> SDK：否；API：是的。 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> 2 </li><li> **說明：**<br/>內容內章節的位置(索引、整數)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>position) </li> <li> **心率：**<br/> (l：串流：panic_ pos) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節位置 </li> <li> **上下文資料：**<br/> (a. media. page。<br/>position) </li> <li> **資料饋送:**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>position) </li> </ul> |

### 章節位移

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 索引鍵:**<br/>media.chapter.offset </li> <li> **需要：**<br/> SDK：否；API：是的。 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> 58 </li><li> **說明：**<br/>內容內的章節偏移(以秒為單位)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>offset) </li> <li> **心率：**<br/> (l：串流：panic_ offset) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節位移 </li> <li> **上下文資料：**<br/> (a. media. page。<br/>offset) </li> <li> **資料饋送:**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>offset) </li> </ul> |

### 章節長度

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.chapter.length </li> <li> **需要：**<br/> SDK：否；API：是的。 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> 486 </li><li> **說明：**<br/>章節長度，以秒為單位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>length) </li> <li> **心率：**<br/> (l：串流：preview_ length) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>章節長度 </li> <li> **上下文資料：**<br/> (a. media. page。<br/>length) </li> <li> **資料饋送:**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>length) </li> </ul> |

### 章節

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>章節的自動產生ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>名稱) </li> <li> **心率：**<br/> (s：串流：panic_ id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>章節 </li> <li> **上下文資料：**<br/> (a. media. page。<br/>名稱) </li> <li> **資料饋送:**<br/>videochapter </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>名稱) </li> </ul> |

## 章節量度 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 章節開始

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **伴隨傳送:**<br/>章節開始 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> TRUE </li><li> **說明：**<br/>章節的開始數。重要: 若此事件已設定，則唯一可能的值為「TRUE」。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>檢視) </li> <li> **心率：**<br/> (s：event：<br/>type= paper_ start) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱：**<br/> 章節開始g </li> <li> **上下文資料：**<br/> (a. media. page。<br/>檢視) </li> <li> **資料饋送:**<br/>videochapterstart </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>檢視) </li> </ul> |

### 章節完成

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3</li> <li> **範例值：**<br/> TRUE </li><li> **說明：**<br/>章節的數目已完成。重要: 若此事件已設定，則唯一可能的值為「TRUE」。若此事件未設定，則不會傳送值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>complete) </li> <li> **心率：**<br/> (s：event：<br/>type= paper_ complete) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱：**<br/> 章節完成g </li> <li> **上下文資料：**<br/> (a. media. page。<br/>complete) </li> <li> **資料饋送:**<br/>videochaptercomplete </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>complete) </li> </ul> |

### 章節逗留時間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定  </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 章節關閉 </li> <li> **最小 SDK 版本:** 1.3 </li> <li> **範例值：**<br/> </li><li> **說明：**<br/>章節逗留時間。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/>**發行日期: 2018 年 9 月 13 日**   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. page。<br/>TimePlayed) </li> <li> **心率:**<br/> </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱：**<br/> 章節逗留時間g </li> <li> **上下文資料：**<br/> (a. media. page。<br/>TimePlayed) </li> <li> **資料饋送:**<br/>videochaptertime </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. page。<br/>TimePlayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
