---
title: 音訊與視訊參數
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 音訊與視訊參數{#audio-and-video-parameters}

>[!IMPORTANT]
>
>在2019年2月7日，Adobe Analytics for Video and Audio發佈量度名稱變更。 <i>媒體起始</i>將更名為<i>媒體開始次數</i>。這項變更是為了在量度和報告中反映業界標準，並讓量度在報告中更容易識別。

>[!NOTE]
>
>從2018年9月13日開始，對某些維度、量度和報表的標籤進行變更，以便跨內容追蹤視訊和音訊分析。 變更的標籤包括: *視訊起始*&#x200B;變更為&#x200B;*媒體起始*、*視訊長度*&#x200B;變更為&#x200B;*內容長度*、*視訊名稱*&#x200B;變更為&#x200B;*內容名稱*。Reports and Analytics 中的視訊報表已全數更新，捨棄「視訊」一名而改用「媒體」。標籤變更並未改變資料收集或歷史資料。如果您要在報表建立工具或其他任何受到前述變更影響的外部自動化資料提取中使用這些標籤，請多加留意。

本主題介紹音訊與視訊內容資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作:**&#x200B;實作數值和要求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本音訊與視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *傳送方式* -指出資料的傳送時間：媒 *體開始* (Media Start)是媒體開始時傳送的分析呼叫， *廣告開始(* Ad Start)是廣告開始時傳送的分析呼叫，等等；關閉呼 *叫* ，是指在媒體作業階段結束時或廣告結束時，從心率伺服器直接傳送至分析伺服器的編譯分析呼叫。 關閉呼叫在網路資料包呼叫中不可用。
   * *最小 SDK 版本* - 指出您存取參數所需的 SDK 版本。
   * *範例值* - 提供常見的變數使用方法範例。
* **網路參數:**&#x200B;顯示傳遞至 Adobe Analytics 或心率伺服器的數值。本欄顯示可於網路呼叫中看到，且由 Adobe Media SDK 產生的參數名稱。
* **報表:**&#x200B;關於如何檢視和分析音訊與視訊資料的資訊。
   * *可用* - 指出資料是否已由報表預設提供 (*是*)，或是需要自行設定 (*自訂*)
   * *預留變數* - 指出資料在預留變數中是否被當作事件、eVar、prop 或分類擷取。
   * *到期* - 指示資料是否會在每次點擊或每次造訪後到期。
   * *報表名稱* - 適用於變數的 Adobe Aanlytics 報表名稱
   * *內容資料* - 傳遞至報表伺服器以及用於處理規則的 Adobe Aanlytics 內容資料名稱。
   * *資料饋送* - 可在 Clickstream 或 Live Stream 資料饋送中找到的變數欄位名稱
   * *Audience Manager* - Adobe Audience Manager 中的特徵名稱

>[!IMPORTANT]
>
>請勿變更下列任何變數的分類名稱，這些變數在「報告／保留變數」下描述為「分類」。\
>媒體分類是在報表套裝啟用媒體追蹤時定義的。 Adobe會不時新增屬性，當發生此情況時，客戶必須重新啟用其報表套裝，才能存取新的媒體屬性。 在更新程式中，Adobe會檢查變數的名稱，以判斷分類是否啟用。 如果其中有遺失，Adobe會再次新增遺失的。

## 核心音訊與視訊資料 {#core-audio-and-video-data}

### 資料流類型 {#stream-type}

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.streamType </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：2.2適用 <br/><br/>於 [Media Collection API概觀或](/help/media-collection-api/mc-api-overview.md) 下載SDK - 2.2版 [](/help/sdk-implement/download-sdks.md)。  </li>  <li> **範例值:** <br/>"video" </li> <li> ****<br/> 說明：識別串流類型。 有效值為 "audio"、"video" 及 ""。<br/><br/>[報告區段](/help/metrics-and-metadata/segments.md):媒 <br/><br/>體串流類型：全部——分 <br/>段所有媒體串流資料；規則：內容(ID)存在媒 <br/><br/>體串流類型：音訊——將 <br/>所有音訊串流資料分段；規則：內容(ID)存在，媒體串流類型=音訊媒 <br/><br/>體串流類型：「視訊」-將所 <br/>有視訊串流資料分段；規則：內容(ID)存在，媒體串流類型！= audio <br/><br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.streamType) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> ****<br/> 上下文資料：(a.media.streamType) </li> <li> **資料饋送:** <br/>videostreamtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.id </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"4586695ABC" </li> <li>****<br/> 說明：內容的內容ID，可用來連結回其他產業/CMS ID，等於 `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> 心率：(s:asset:video_id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> ****<br/> 上下文資料：(a.media.name) </li> <li> **資料饋送:**<br/>影片 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容長度 (變數)

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.length </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：VOD:128;即時：86400;線性：1800。 </li><li> ****<br/> 說明：剪輯長度／執行時期——這是所使用內容的最大長度（或持續時間）（以秒為單位）。 It equals the last value of `l:asset:length` from events of type Main. <br/>如果 `l:asset:length` 未設定，則會使用的最 `l:asset:duration` 後一個值。 <br/>在報告中，視訊長度是分類，而內容長度（變數）是eVAR。  <br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。<br/>1.5.1版之前的版本是 `l:asset:duration`;在1.5.1之後，這是 `l:asset:length.`<br/> **發行日期: 2018 年 9 月 13 日** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 心率：(l:asset:length) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 內容長度 (變數) </li> <li> ****<br/> 上下文資料：(a.media.length) </li> <li> **資料饋送:**<br/>videolength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 影片長度

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.length </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：VOD:128;即時：86400;線性：1800。 </li> <li> ****<br/> 說明：剪輯長度／執行時期——這是所使用內容的最大長度（或持續時間）（以秒為單位）。 It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 心率：(l:asset:length) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 視訊長度 </li> <li> ****<br/> 上下文資料：(a.media.length) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.contentType </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>限制字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"vod" </li> <li> ****<br/> 說明：每個串流類型 **的可用值**: <br/> _音訊:_ "song"、"podcast"、"audiobook"、"radio" <br/> __ 影片：「VoD」、「Live」、「Linear」、「UGC」、「DVoD」 <br/> 客戶可為此參數提供自訂值。 這等於 `s:stream:type.` 如果未設定，則等於 `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.contentType) </li> <li> ****<br/> 心率：(s:stream:type) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容類型 </li> <li> ****<br/> 上下文資料：(a.contentType) </li> <li> **資料饋送:**<br/>videocontenttype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 媒體工作階段 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>取自後端 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.8 </li> <li> ****<br/> 範例值：1482236761294786918253 </li> <li> ****<br/> 說明：這可識別個別播放所獨有的內容串流的例項。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.vsid) </li> <li> ****<br/> 心率：(s:event:sid) </li> </ul> | <ul> <li> **可用性:**<br/>使用處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.vsid) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vsid) </li> </ul> |

### 媒體下載標幟

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> `config.downloadedcontent` </li> <li> **API 索引鍵:**<br/>取自後端 </li> <li> **必要:**<br/>否 </li> <li> ****<br/> 類型：布林值 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：啟 <br/>動Android和iOS擴充功能v1.1.0 </li> <li> ****<br/> 範例值：true </li> <li> ****<br/> 說明：當因播放下載的內容媒體作業而產生點擊時，設為true。 未播放下載的內容時不存在。<br/><br/>[啟動](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.downloaded) </li> <li> ****<br/> 心率：(s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.downloaded) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### 內容播放器名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.playerName </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值："Brightcove" </li> <li> ****<br/> 說明：播放器的名稱。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media)。<br/>playerName) </li> <li> ****<br/> 心率：(s:sp:player_name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容播放器名稱 </li> <li> ****<br/> 上下文資料：(a.media.playerName) </li> <li> **資料饋送:**<br/>ideoplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.playerName) </li> </ul> |

### 內容頻道

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.channel </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"Sports" </li> <li> ****<br/> 說明：散發站／頻道或內容播放位置。 此處接受的任何字串值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.channel) </li> <li> ****<br/> 心率：(s:sp:channel) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容管道 </li> <li> ****<br/> 上下文資料：(a.media.channel) </li> <li> **資料饋送:**<br/>videochannel </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.channel) </li> </ul> |

### 內容區段

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值："0-10" </li> <li> ****<br/> 說明：說明已檢視內容部分的間隔（以分鐘為單位）。 此區段的計算方式為播放工作階段期間播放點值的最大值與最小值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容區段 </li> <li> ****<br/> 上下文資料：(a.media.segment) </li> <li> **資料饋送:**<br/>videosegment </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segment) </li> </ul> |

### 內容名稱 (變數)

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.name </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> **範例值:** <br/>"The Big Bang Theory" </li> <li> **說明：**<br/>`s:asset:name.`<br/>這是內容的「好記」（人工可讀）名稱，等於「在報表中」的最後一個值，「視訊名稱」是分類，「內容名稱」（變數）是eVAR。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media)。<br/>好記名稱) </li> <li> ****<br/> 心率：(s:asset:name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 內容名稱 (變數) </li> <li> ****<br/> 上下文資料：(a.media.friendlyName) </li> <li> **資料饋送:**<br/>videoname </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 影片名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.name </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> **範例值:** <br/>"The Big Bang Theory" </li> <li> ****<br/> 說明：這是內容的「好記」（人類可讀）名稱，等於報告中的最後一個值，「視訊名稱」是分類，「內容名稱」（變數）是eVAR。 `s:asset:name.`<br/> <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media)。<br/>好記名稱) </li> <li> ****<br/> 心率：(s:asset:name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 視訊名稱 </li> <li> ****<br/> 上下文資料：(a.media.friendlyName) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### 視訊路徑

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"4586695ABC" </li> <li> ****<br/> 說明：提供追蹤檢視器在網站和／或應用程式中的路徑，以查看他們檢視特定視訊所採用的路徑的能力。 任何整數和/或字母的組合。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> 心率：(s:asset:video_id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **保留變數:**<br/>prop </li> <li> **報表名稱:**<br/>視訊路徑 </li> <li> ****<br/> 上下文資料：(a.media.name) </li> <li> **資料饋送:**<br/>videopath </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK 版本

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.sdkVersion </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"2.62.0_release" </li> <li> ****<br/> 說明：播放器使用的SDK版本。 您可以採用播放器適用的自訂值。<br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media)。<br/>sdk版本) </li> <li> ****<br/> 心率：(s:sp:sdk) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.sdkVersion) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 版本

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> 說明：用於追蹤工作階段的Media SDK版本。 <br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media)。<br/>vhlVersion) </li> <li> ****<br/> 心率：(s:sp:hb_version) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.vhlVersion) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 標準音訊和視訊中繼資料 {#standard-audio-and-video-metadata}

### Show

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SHOW </li> <li> **API 索引鍵:**<br/>media.show </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："現代家庭""黑名單""新女孩" </li> <li> ****<br/> 說明：只有當顯示為系 <br/>列的一部分時，才需要程式／系列名稱程式名稱。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.show) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>節目 </li> <li> ****<br/> 上下文資料：(a.media.show) </li> <li> **資料饋送:**<br/>videoshow </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.show) </li> </ul> |

### 資料流格式

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>STREAM_FORMAT </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"Live" </li> <li> ****<br/> 說明：串流的格式（即時、VOD、線性）。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.format) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.format) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.format) </li> </ul> |

### 季數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SEASON </li> <li> **API 索引鍵:**<br/>media.season </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："2" </li> <li> ****<br/> 說明：節目所屬的季號。  只有當該節目屬於系列時，才需要「季節系列」。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.season) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>季數 </li> <li> ****<br/> 上下文資料：(a.media.season) </li> <li> **資料饋送:**<br/>videoseason </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.season) </li> </ul> |

### 集數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>EPISODE </li> <li> **API 索引鍵:**<br/>media.episode </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："13" </li> <li> ****<br/> 說明：情節的數目。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ipesote) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.ipesote) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>集數 </li> <li> ****<br/> 上下文資料：(a.media.ipesote) </li> <li> **資料饋送:**<br/>videoepisode </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.episode) </li> </ul> |

### 資產 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>ASSET_ID </li> <li> **API 索引鍵:**<br/>media.assetId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：《89745363》 </li> <li> ****<br/> 說明：這是媒體資產內容的唯一識別碼，例如電視系列集合識別碼、影片資產識別碼或即時事件識別碼。 一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.asset) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>資產 ID </li> <li> ****<br/> 上下文資料：(a.media.asset) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.asset) </li> </ul> |

### 類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>GENRE </li> <li> **API 索引鍵:**<br/>media.genre </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：《戲劇》、《喜劇》 </li> <li> ****<br/> 說明：依內容製作者的定義，輸入或分組內容。 應在實作變數時以逗號分隔這些值。在報表中，eVar 清單會將每個值拆分到行項目中，每個行項目接受同樣的量度加權。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.genre) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **保留變數:**<br/>eVar 清單 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>類型 </li> <li> ****<br/> 上下文資料：(a.media.genre) </li> <li> **資料饋送:**<br/>videogenre </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.genre) </li> </ul> |

### 首播日期

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FIRST_AIR_DATE </li> <li> **API 索引鍵:**<br/>media.firstAirDate </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：《2016-01-25》 </li> <li> ****<br/> 說明：內容首次在電視上播放的日期。 任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.airDate) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 首播日期 </li> <li> ****<br/> 上下文資料：(a.media.airDate) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.airDate) </li> </ul> |

### 首次數位化日期

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FIRST_DIGITAL_DATE </li> <li> **API 索引鍵:**<br/>media.firstDigitalDate </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：《2016-01-25》 </li> <li> ****<br/> 說明：任何數位頻道或平台首次播放內容的日期。 任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.digitalDate) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/> 首次數位化日期 </li> <li> ****<br/> 上下文資料：(a.media.digitalDate) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### 內容評等

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>RATING </li> <li> **API 索引鍵:**<br/>media.rating </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：電視台，電視台，電視台，電視台 </li> <li> ****<br/> 說明：依「TV家長准則」所定義的分級。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.rating) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>內容分級 </li> <li> ****<br/> 上下文資料：(a.media.rating) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.rating) </li> </ul> |

### 創作者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>ORIGINATOR </li> <li> **API 索引鍵:**<br/>media.originator </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值：「華納兄弟」、「索尼」、「迪士尼」 </li> <li> ****<br/> 說明：內容的製作者。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.originator) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/> 創作者 </li> <li> ****<br/> 上下文資料：(a.media.originator) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.originator) </li> </ul> |

### 網路

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>NETWORK </li> <li> **API 索引鍵:**<br/>media.network </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："Fox"、"Bravo"、"ESPN" </li> <li> ****<br/> 說明：網路／頻道名稱。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.network) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>網路 </li> <li> ****<br/> 上下文資料：(a.media.network) </li> <li> **資料饋送:**<br/>videonetwork </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.network) </li> </ul> |

### 節目類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SHOW_TYPE </li> <li> **API 索引鍵:**<br/>media.showType </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："0" =整集；"1" =預覽／預告片；"2" =剪輯；"3" =其他。 </li> <li> ****<br/> 說明：內容類型，以0到3之間的整數表示。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.type) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>節目類型 </li> <li> ****<br/> 上下文資料：(a.media.type) </li> <li> **資料饋送:**<br/>videoshowtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>MVPD </li> <li> **API 索引鍵:**<br/>media.pass.mvpd </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："Comcast"、"DirecTV"、"Dish" </li> <li> ****<br/> 說明：透過Adobe驗證提供的MVPD。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.mvpd) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>MVPD </li> <li> ****<br/> 上下文資料：(a.media.pass.mvpd) </li> <li> **資料饋送:**<br/>videomvpd </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 已驗證

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>AUTHORIZED </li> <li> **API 索引鍵:**<br/>media.pass.auth </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："TRUE" </li> <li> ****<br/> 說明：使用者已透過Adobe驗證獲得授權。  <br/>**重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.auth) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.pass.<br/>驗證) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱名稱:**<br/>已授權 </li> <li> ****<br/> 上下文資料：(a.media.pass.auth) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 時段

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>DAY_PART </li> <li> **API 索引鍵:**<br/>media.dayPart </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> </li> <li> ****<br/> 說明：定義播放或播放內容當天時間的屬性。 可由客戶按照需求設定任何值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.dayPart) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>時段 </li> <li> ****<br/> 上下文資料：(a.media.dayPart) </li> <li> **資料饋送:**<br/>videodaypart </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### 媒體摘要類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FEED </li> <li> **API 索引鍵:**<br/>media.feed </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> ****<br/> 範例值："East-HD"、"West-HD"、"East-SD" </li> <li> ****<br/> 說明：動態消息類型。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.feed) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>媒體摘要類型 </li> <li> ****<br/> 上下文資料：(a.media.feed) </li> <li> **資料饋送:**<br/>videofeedtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.feed) </li> </ul> |

### 藝人

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.artist </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"The Beatles" </li> <li> ****<br/> 說明：藝術家的名字。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.artist) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.artist) </li> <li> **資料饋送:** <br/>videoaudioartist </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.artist) </li> </ul> |

### 專輯

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.album </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:**<br/>"Revolver" </li> <li> ****<br/> 說明：相簿的名稱。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.album) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.album) </li> <li> **資料饋送:** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.album) </li> </ul> |

### 標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.label </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:**<br/>"Revolver" </li> <li> ****<br/> 說明：記錄標籤的名稱。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.label) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.label) </li> <li> **資料饋送:** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.label) </li> </ul> |

### 作者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.author </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"John Kennedy Toole" </li> <li> ****<br/> 說明：作者（音像書）的名稱。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.author) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.author) </li> <li> **資料饋送:** <br/>videoaudioauthor </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.author) </li> </ul> |

### 電台

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.station </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"NPR" </li> <li> ****<br/> 說明：無線電站的名稱/ ID。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.station) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.station) </li> <li> **資料饋送:**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.station) </li> </ul> |

### 發行者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.publisher </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體開始，媒體關閉 </li> <li> **最小 ** SDK版本：1.5.7可在 <br/>Media Collection概觀 [或下載SDK](/help/media-collection-api/mc-api-overview.md) - [2.2版中取得](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"Random Bauhaus" </li> <li> ****<br/> 說明：音訊內容發佈者的名稱。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.publisher) </li> <li> ****<br/> 心率：(s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> ****<br/> 上下文資料：(a.media.publisher) </li> <li> **資料饋送:**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.publisher) </li> </ul> |

## 音訊與視訊量度 {#audio-and-video-metrics}

### 媒體開始次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定</li> <li> **API 索引鍵:**<br/>不適用</li> <li> **類型:**<br/>字串</li> <li> ****<br/> 傳送方式：媒體開始</li> <li> **最小 SDK 版本:**&#x200B;任何版本</li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：載入媒體的事件。 (觀看者按下&#x200B;_「播放」_&#x200B;按鈕時，即會發生此情形。)即使是前段廣告、緩衝、錯誤等也會計入此值。<br/>**重要:** 如果已設定，則此值只能是 true。If it is not set, no value is returned.  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.view) </li> <li> ****<br/> 心率：(s:event:<br/>type=start) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> ****<br/> 報表名稱：媒體開始 </li> <li> ****<br/> 上下文資料：(a.media.view) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.view) </li> </ul> |

### 內容開始

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：使用第一個媒體影格。 If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容開始 </li> <li> ****<br/> 上下文資料：(a.media.play) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.play) </li> </ul> |

### 內容完成 {#content-complete}

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：被觀看完成的串流。 這並不一定表示使用者觀看或聆聽整個串流；他們本可以跳到前面去。 這隻表示使用者已到達串流的結尾，100%。 <br/>另請參閱 [會話結束](quality-parameters.md#session-end)<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> ****<br/> 心率：(s:event:<br/>type=complete) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容完成 </li> <li> ****<br/> 上下文資料：(a.media.complete) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.complete) </li> </ul> |

### 內容逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：105 </li> <li> ****<br/> 說明：總和主要內容上PLAY類型所有事件的事件持續時間（以秒為單位）。  該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容逗留時間 </li> <li> ****<br/> 上下文資料：(a.media.timePlayed) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### 媒體逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：120 </li> <li> ****<br/> 說明：總和主要和廣告內容類型PLAY的所有事件的事件持續時間（以秒為單位）。  該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/> 媒體逗留時間 </li> <li> ****<br/> 上下文資料：(a.media.totalTimePlayed) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### 不重複播放時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：94 </li> <li> ****<br/> 說明：在作業期間播放之內容之唯一區段的數秒值。 不包括觀看者向前尋找，並多次觀看同一個內容區段時的播放時間。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.uniqueTimePlayed) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10 %進度標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：播放頭會根據長度傳遞10%的內容標籤。 此標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>10% 進度標記 </li> <li> ****<br/> 上下文資料：(a.media.progress10) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25%進度標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：Playhead會根據內容長度傳遞25%的內容標籤。 標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>25% 進度標記 </li> <li> ****<br/> 上下文資料：(a.media.progress25) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50%進度標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：Playhead會根據內容長度傳遞50%的內容標籤。 標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>50% 進度標記 </li> <li> ****<br/> 上下文資料：(a.media.progress50) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75%進度標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> **不適用** </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：Playhead會根據內容長度傳遞75%的內容標籤。 標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>75% 進度標記 </li> <li> ****<br/> 上下文資料：(a.media.progress75) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 %進度標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：Playhead會根據內容長度傳遞95%的內容標籤。 標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>95% 進度標記 </li> <li> ****<br/> 上下文資料：(a.media.progress95) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress95) </li> </ul> |

### 平均每分鐘觀眾

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>大於或等於 1 </li> <li> ****<br/> 說明：「平均每分鐘觀眾」度量會計算為特定媒體項目的「總內容逗留時間」，除以其所有播放作業的長度： <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **範例值:**<br/>平均每分鐘觀眾 </li> <li> ****<br/> 上下文資料：(a.media.averageMinuteAudience) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 同盟資料

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> ****<br/> 類型：布林值 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：true  </li> <li> ****<br/> 說明：當點擊為同盟時（即客戶作為同盟資料共用的一部分而收到，而非自己的實作），設為true。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>不適用 </li> <li> ****<br/> 上下文資料：(a.media.federated) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.federated) </li> </ul> |

### 預估資料流量

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> ****<br/> 範例值：1 —— 播放19分鐘； <br/>2 —— 播放31分鐘； <br/>3 —— 播放78分鐘。 </li> <li> ****<br/> 說明：每個個別內容的估計視訊或音訊串流數。 播放時間 (內容 + 廣告) 每 30 分鐘這個值就會增加。客戶必須建立自己的處理規則，才能有可用於報告的值。<br/><br/>根據（或totalTimePlayed =視訊總時間），每30分鐘計 `ms_s` 算一個串流，類似於： <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> ****<br/> 上下文資料：(a.media.estimatedStreams) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### 暫停的受影響資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：此值為true或false。 It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> ****<br/> 心率：(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>暫停的受影響資料流 </li> <li> ****<br/> 上下文資料：(a.media.pause) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pause) </li> </ul> |

### 暫停事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> ****<br/> 範例值：2 </li> <li> ****<br/> 說明：此度量的計算方式為播放作業階段期間發生的暫停期間計數。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> ****<br/> 心率：(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>暫停事件 </li> <li> ****<br/> 上下文資料：(a.media.pauseCount) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 總暫停期間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> ****<br/> 範例值：190 </li> <li> ****<br/> 說明：總和PAUSE類型所有事件的持續時間（以秒為單位）。 該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>總暫停期間 </li> <li> ****<br/> 上下文資料：(a.media.pauseTime) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### 內容恢復

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> **media.resume** </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：每次在超過30分鐘的緩衝、暫停或停止期間後繼續的播放，或者，如果此值是由播放器在VideoInfo trackPlay上設定，則會計為「繼續」。 <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> ****<br/> 心率：(s:event:<br/>type=resume) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容恢復 </li> <li> ****<br/> 上下文資料：(a.media.resume) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.resume) </li> </ul> |

### 內容區段檢視次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> ****<br/> 傳送方式：媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> ****<br/> 說明：主要內容的檢視次數。 A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容區段檢視次數 </li> <li> ****<br/> 上下文資料：(a.media.segmentView) </li> <li> **資料饋送:**<br/>不適用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segmentView) </li> </ul> |

<!--
### Ad Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.adCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.chapterCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |
-->

## 加州消費者隱私權法案(CCPA)參數 {#ccpa-params}

### 選擇退出伺服器端轉發

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK金鑰：不適用 </li> <li> ****<br/>  API金鑰：analytics.optOutServerSideForwarding </li> <li> **必要:**<br/>否 </li> <li> ****<br/> 類型：布林值 </li> <li> ****<br/> 傳送方式：媒體開始 </li> <li> **最小 ** SDK版本：不適用 </li> <li> ****<br/> 範例值：true </li> <li>****<br/> 說明：當使用者選擇不在Adobe Analytics和其他Experience cloud解決方案（例如Audience Manager）之間共用資料時，設為true。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.dmp) </li> <li> ****<br/> 心率：(s:meta:cm.ssf) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> ****<br/> 上下文資料：不適用 </li> <li> **資料饋送:**<br/>影片 </li> <li> ****<br/> Audience Manager:不適用 </li> </ul> |

### 選擇退出分享

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK金鑰：不適用 </li> <li> ****<br/>  API金鑰：analytics.optOutShare </li> <li> **必要:**<br/>否 </li> <li> ****<br/> 類型：布林值 </li> <li> ****<br/> 傳送方式：媒體開始 </li> <li> **最小 ** SDK版本：不適用 </li> <li> ****<br/> 範例值：true </li> <li>****<br/> 說明：當使用者選擇退出其資料的同盟時（例如其他Adobe Analytics用戶端），設為true。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.oos) </li> <li> ****<br/> 心率：(s:meta:cm.oos) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> ****<br/> 上下文資料：不適用 </li> <li> **資料饋送:**<br/>影片 </li> <li> ****<br/> Audience Manager:不適用 </li> </ul> |

## 相關API {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

