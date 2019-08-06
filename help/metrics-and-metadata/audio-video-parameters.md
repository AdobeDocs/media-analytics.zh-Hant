---
seo-title: 音訊與視訊參數
title: 音訊與視訊參數
uuid: fdacfb8b-db3 e-46fb-b9 ad-c3 a749555 b2 a
translation-type: tm+mt
source-git-commit: a9e1c8ba7c8a95120e4c66460ff6d742c0855652

---


# 音訊與視訊參數{#audio-and-video-parameters}

>[!IMPORTANT]
>
>在2019年月日，Adobe Analytics for Video和Audio發行了度量名稱變更。<i>媒體起始</i>將更名為<i>媒體開始次數</i>。這項變更是為了反映度量和報告中的業界標準，並讓量度便於識別，以便在報告中識別。

>[!NOTE]
>
>自2018年月13日起，針對部分維度、度量和報告進行標籤變更，允許跨內容追蹤視訊和音訊分析。變更的標籤包括: *視訊起始*&#x200B;變更為&#x200B;*媒體起始*、*視訊長度*&#x200B;變更為&#x200B;*內容長度*、*視訊名稱*&#x200B;變更為&#x200B;*內容名稱*。Reports and Analytics 中的視訊報表已全數更新，捨棄「視訊」一名而改用「媒體」。標籤變更並未改變資料收集或歷史資料。如果您要在報表建立工具或其他任何受到前述變更影響的外部自動化資料提取中使用這些標籤，請多加留意。

本主題介紹音訊與視訊內容資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作:**&#x200B;實作數值和要求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本音訊與視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *隨附於* -表示傳送資料時： *媒體開始* 是在媒體開始時傳送的分析呼叫， *廣告開始* 是在廣告開始時傳送的分析呼叫等等； *關閉* 呼叫是直接從心率伺服器傳送至媒體工作階段結束處的編譯分析呼叫，或是廣告、章節等結尾的編譯分析呼叫。網路封包呼叫無法使用關閉呼叫。
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
>請勿變更以下任何列於「報告/保留變數」下方的變數分類名稱，作為「分類」。\
>媒體分類是在報告套裝啓用媒體追蹤時定義。Adobe會不時新增屬性，當發生這種情況時，客戶必須重新啓用報表套裝，才能存取新媒體屬性。在更新過程中，Adobe會檢查變數名稱，判斷分類是否啓用。如果其中有任何項目遺失，Adobe會再次新增遺漏的項目。

## 核心音訊與視訊資料 {#section_y55_y1m_n1b}

### 資料流類型 {#stream-type}

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.streamType </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 2.2 <br/><br/>適用於 [Media Collection API概觀](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li>  <li> **範例值:** <br/>"video" </li> <li> **說明：**<br/> 識別串流類型。有效值為 "audio"、"video" 及 ""。<br/><br/>[報告區段](/help/metrics-and-metadata/segments.md)： <br/><br/>媒體串流類型：全部- <br/>區段所有媒體串流資料；規則：內容(ID)存在 <br/><br/>媒體串流類型：音訊- <br/>區段所有音訊串流資料；規則：內容(ID)存在，且媒體串流類型=音訊 <br/><br/>媒體串流類型：「視訊」- <br/>區段所有視訊串流資料；規則：內容(ID)存在和媒體串流類型！= audio <br/><br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. StreamType) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. streamType) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> **上下文資料：**<br/> (a. media. StreamType) </li> <li> **資料饋送:** <br/>videostreamtype </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容 ID

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.id </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"4586695ABC" </li> <li>**說明：**<br/> 內容的內容ID，可用來連結至其他產業/CMS ID，等於 `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. name) </li> <li> **活動訊號：**<br/> (s：資產：video_ id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>造訪時 </li> <li> **報表名稱:**<br/>內容 </li> <li> **上下文資料：**<br/> (a. media. name) </li> <li> **資料饋送:**<br/>影片 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容長度 (變數)

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.length </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> VOD：128；即時：86400；線性：1800. </li><li> **說明：**<br/> 剪輯段長度/執行時期-這是所要消耗的內容長度上限(以秒為單位)。It equals the last value of `l:asset:length` from events of type Main. <br/>`l:asset:length` 如果未設定，則會使用最後 `l:asset:duration` 一個值。<br/>在報告中，視訊長度是分類，而內容長度(變數)是eVar。 <br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。<br/>1.5.1版之前即 `l:asset:duration`為；1.5.1之後，此為 `l:asset:length.`<br/> **發行日期: 2018 年 9 月 13 日** </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. length) </li> <li> **活動訊號：**<br/> (l：資產：長度) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 內容長度 (變數) </li> <li> **上下文資料：**<br/> (a. media. length) </li> <li> **資料饋送:**<br/>videolength </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 影片長度

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.length </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> VOD：128；即時：86400；線性：1800. </li> <li> **說明：**<br/> 剪輯段長度/執行時期-這是所要消耗的內容長度上限(以秒為單位)。It equals the last value of `l:asset:length` from events of type Main. `l:asset:length` 如果未設定，則會使用最後 `l:asset:duration` 一個值。In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. length) </li> <li> **活動訊號：**<br/> (l：資產：長度) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 視訊長度 </li> <li> **上下文資料：**<br/> (a. media. length) </li> <li> **資料饋送:** <br/>videoclassificationlength </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 內容類型

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.contentType </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>限制字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"vod" </li> <li> **說明：**<br/>**每個串流類型的可用值**： <br/> _音訊:_ "song"、"podcast"、"audiobook"、"radio" <br/> _影片：_ 「VOD」、「Live」、「線性」、「UGC」、「DVOD」 <br/> 客戶可以為此參數提供自訂值。此等於 `s:stream:type.` 如果未設定，則等於 `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. contentType) </li> <li> **活動訊號：**<br/> (s：串流：type) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容類型 </li> <li> **上下文資料：**<br/> (a. contentType) </li> <li> **資料饋送:**<br/>videocontenttype </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 媒體工作階段 ID

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>取自後端 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.8 </li> <li> **範例值：**<br/> 148223661294786925253 </li> <li> **說明：**<br/> 這可識別個別播放專屬內容串流的例項。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. vsid) </li> <li> **心率：**<br/> (s：event：sid) </li> </ul> | <ul> <li> **可用性:**<br/>使用處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> **上下文資料：**<br/> (a. media. vsid) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.vsid) </li> </ul> |

### 內容播放器名稱

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.playerName </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> 「Brightcove」 </li> <li> **說明：**<br/> 播放器的名稱。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>playerName) </li> <li> **活動訊號：**<br/> (s：sp：player_ name) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容播放器名稱 </li> <li> **上下文資料：**<br/> (a. media. playerName) </li> <li> **資料饋送:**<br/>ideoplayername </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.playerName) </li> </ul> |

### 內容頻道

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.channel </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"Sports" </li> <li> **說明：**<br/> 散髮站/頻道或內容播放地點。此處接受的任何字串值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. channel) </li> <li> **活動訊號：**<br/> (s：sp：channel) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容管道 </li> <li> **上下文資料：**<br/> (a. media. channel) </li> <li> **資料饋送:**<br/>videochannel </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.channel) </li> </ul> |

### 內容區段

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>是 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> 「0-10」 </li> <li> **說明：**<br/> 描述已檢視內容之部分的間隔(在幾分鐘內)。此區段的計算方式為播放工作階段期間播放點值的最大值與最小值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>內容區段 </li> <li> **上下文資料：**<br/> (a. media. segment) </li> <li> **資料饋送:**<br/>videosegment </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.segment) </li> </ul> |

### 內容名稱 (變數)

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/>media.name </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> **範例值:** <br/>"The Big Bang Theory" </li> <li> **說明：**<br/>此為內容的「好記」(人類可讀取)名稱，等於報告 `s:asset:name.`<br/>中的最後一個值，視訊名稱為分類，而內容名稱(變數)為eVar。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>friendlyName) </li> <li> **活動訊號：**<br/> (s：資產：名稱) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 內容名稱 (變數) </li> <li> **上下文資料：**<br/> (a. media. friendlyName) </li> <li> **資料饋送:**<br/>videoname </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 影片名稱

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.name </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.1 </li> <li> **範例值:** <br/>"The Big Bang Theory" </li> <li> **說明：**<br/> 此為內容的「好記」(人類可讀取)名稱，等於報告 `s:asset:name.`<br/>中的最後一個值，視訊名稱為分類，而內容名稱(變數)為eVar。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>friendlyName) </li> <li> **活動訊號：**<br/> (s：資產：名稱) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 視訊名稱 </li> <li> **上下文資料：**<br/> (a. media. friendlyName) </li> <li> **資料饋送:** <br/>videoclassificationname </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.friendlyName) </li> </ul> |

### 視訊路徑

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:** <br/>"4586695ABC" </li> <li> **說明：**<br/> 提供追蹤檢視器跨網站和/或應用程式路徑的能力，以檢視他們檢視特定視訊所採用的路徑。任何整數和/或字母的組合。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. name) </li> <li> **活動訊號：**<br/> (s：資產：video_ id) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **保留變數:**<br/>prop </li> <li> **報表名稱:**<br/>視訊路徑 </li> <li> **上下文資料：**<br/> (a. media. name) </li> <li> **資料饋送:**<br/>videopath </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.name) </li> </ul> |

### SDK 版本

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/>media.sdkVersion </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"2.62.0_release" </li> <li> **說明：**<br/> 播放器使用的SDK版本。您可以採用播放器適用的自訂值。<br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>SDKVersion) </li> <li> **活動訊號：**<br/> (s：sp：sdk) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. SDKVersion) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 版本

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"js-2.0.1.88-c8c0b1" </li> <li> **說明：**<br/> 用於追蹤工作階段的Media SDK版本。<br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。<br/><br/>[MediaHeartbeat. version()；](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>VHLVersion) </li> <li> **活動訊號：**<br/> (s：sp：hb_ version) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> **上下文資料：**<br/> (a. media. vlVersion) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.vhlVersion) </li> </ul> |

## 標準音訊和視訊中繼資料 {#section_pfc_hbm_n1b}

### Show

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SHOW </li> <li> **API 索引鍵:**<br/>media.show </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「現代系列」「黑名單」「新女孩」 </li> <li> **說明：**<br/> 只有在系列屬於系列時，才需要Program/Series Name <br/>Program Name。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. show) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. show) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>節目 </li> <li> **上下文資料：**<br/> (a. media. show) </li> <li> **資料饋送:**<br/>videoshow </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.show) </li> </ul> |

### 資料流格式

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>STREAM_FORMAT </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:** <br/>"Live" </li> <li> **說明：**<br/> 串流格式(即時、VOD、線性)。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. format) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. format) </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> **上下文資料：**<br/> (a. media. format) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.format) </li> </ul> |

### 季數

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SEASON </li> <li> **API 索引鍵:**<br/>media.season </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「2」 </li> <li> **說明：**<br/> 顯示的季數。只有當系列屬於系列時，才需要「季節系列」。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. monay) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. mondly) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>季數 </li> <li> **上下文資料：**<br/> (a. media. monay) </li> <li> **資料饋送:**<br/>videoseason </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.season) </li> </ul> |

### 集數

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>EPISODE </li> <li> **API 索引鍵:**<br/>media.episode </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「13」 </li> <li> **說明：**<br/> 集區的數目。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. operode) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. operode) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>集數 </li> <li> **上下文資料：**<br/> (a. media. operode) </li> <li> **資料饋送:**<br/>videoepisode </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.episode) </li> </ul> |

### 資產 ID

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>ASSET_ID </li> <li> **API 索引鍵:**<br/>media.assetId </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「89743563」 </li> <li> **說明：**<br/> 這是媒體資產內容的唯一識別碼，例如TV系列集識別碼、影片資產識別碼或即時事件識別碼。一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. asset) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. asset) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>資產 ID </li> <li> **上下文資料：**<br/> (a. media. asset) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.asset) </li> </ul> |

### 類型

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>GENRE </li> <li> **API 索引鍵:**<br/>media.genre </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「戲劇」、「喜劇片」 </li> <li> **說明：**<br/> 輸入或分組內容製作人定義的內容。應在實作變數時以逗號分隔這些值。在報表中，eVar 清單會將每個值拆分到行項目中，每個行項目接受同樣的量度加權。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. genre) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. genre) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **保留變數:**<br/>eVar 清單 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>類型 </li> <li> **上下文資料：**<br/> (a. media. genre) </li> <li> **資料饋送:**<br/>videogenre </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.genre) </li> </ul> |

### 首播日期

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FIRST_AIR_DATE </li> <li> **API 索引鍵:**<br/>media.firstAirDate </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「2016-01-25」 </li> <li> **說明：**<br/> 首次在電視上播送內容的日期。任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. AirDate) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. AirDate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/> 首播日期 </li> <li> **上下文資料：**<br/> (a. media. AirDate) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.airDate) </li> </ul> |

### 首次數位化日期

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FIRST_DIGITAL_DATE </li> <li> **API 索引鍵:**<br/>media.firstDigitalDate </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「2016-01-25」 </li> <li> **說明：**<br/> 內容首次在任何數位頻道或平台上播放的日期。任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. DigitalDate) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. DigitalDate) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/> 首次數位化日期 </li> <li> **上下文資料：**<br/> (a. media. DigitalDate) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.digitalDate) </li> </ul> |

### 內容評等

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>RATING </li> <li> **API 索引鍵:**<br/>media.rating </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> TWY，TVG，TVPG，TVMA </li> <li> **說明：**<br/> 依電視家長准則定義的評分。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. radation) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. ratings) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/>內容分級 </li> <li> **上下文資料：**<br/> (a. media. radation) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.rating) </li> </ul> |

### 創作者

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>ORIGINATOR </li> <li> **API 索引鍵:**<br/>media.originator </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「Warner Brothers」，「Sony」，「Disney」 </li> <li> **說明：**<br/> 內容的創作者。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. riginator) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. riginator) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>分類 </li> <li> **報表名稱:**<br/> 創作者 </li> <li> **上下文資料：**<br/> (a. media. riginator) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.originator) </li> </ul> |

### 網路

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>NETWORK </li> <li> **API 索引鍵:**<br/>media.network </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「Fox」、「Bravo」、「ESPN」 </li> <li> **說明：**<br/> 網路/頻道名稱。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. network) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. network) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>網路 </li> <li> **上下文資料：**<br/> (a. media. network) </li> <li> **資料饋送:**<br/>videonetwork </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.network) </li> </ul> |

### 節目類型

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>SHOW_TYPE </li> <li> **API 索引鍵:**<br/>media.showType </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「0」=完整版；「1」=預覽/預告；「2」= Clip；「3」=其他。 </li> <li> **說明：**<br/> 內容類型，表示為與之間的整數。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. type) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. type) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>節目類型 </li> <li> **上下文資料：**<br/> (a. media. type) </li> <li> **資料饋送:**<br/>videoshowtype </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.type) </li> </ul> |

### MVPD

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>MVPD </li> <li> **API 索引鍵:**<br/>media.pass.mvpd </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「Comcast」，「DirectTV」，「Dh」 </li> <li> **說明：**<br/> 透過Adobe驗證提供的MVPD。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. aspass. mvpd) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. pass。<br/>mvpd) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>MVPD </li> <li> **上下文資料：**<br/> (a. media. aspass. mvpd) </li> <li> **資料饋送:**<br/>videomvpd </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.pass.mvpd) </li> </ul> |

### 已驗證

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>AUTHORIZED </li> <li> **API 索引鍵:**<br/>media.pass.auth </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「TRUE」 </li> <li> **說明：**<br/> 使用者已透過Adobe驗證獲得授權。<br/>**重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. aspass. ah) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. pass。<br/>Auth) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱名稱:**<br/>已授權 </li> <li> **上下文資料：**<br/> (a. media. aspass. ah) </li> <li> **資料饋送:**<br/>videoauthorized </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.pass.auth) </li> </ul> |

### 時段

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>DAY_PART </li> <li> **API 索引鍵:**<br/>media.dayPart </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> </li> <li> **說明：**<br/> 定義內容廣播或播放的時間的屬性。可由客戶按照需求設定任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. dayPart) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. dayPart) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>時段 </li> <li> **上下文資料：**<br/> (a. media. dayPart) </li> <li> **資料饋送:**<br/>videodaypart </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.dayPart) </li> </ul> |

### 媒體摘要類型

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>FEED </li> <li> **API 索引鍵:**<br/>media.feed </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.7 </li> <li> **範例值：**<br/> 「East-HD」、「West-HD」、「East-SD」 </li> <li> **說明：**<br/> 動態消息類型。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. feeds) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. feeds) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報表名稱:**<br/>媒體摘要類型 </li> <li> **上下文資料：**<br/> (a. media. feeds) </li> <li> **資料饋送:**<br/>videofeedtype </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.feed) </li> </ul> |

### 藝人

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.artist </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"The Beatles" </li> <li> **說明：**<br/> 藝術家姓名。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.藝術家) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media.藝術家) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media.藝術家) </li> <li> **資料饋送:** <br/>videoaudioartist </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.artist) </li> </ul> |

### 專輯

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.album </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:**<br/>"Revolver" </li> <li> **說明：**<br/> 相簿名稱。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. backum) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. backum) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. backum) </li> <li> **資料饋送:** <br/>videoaudioalbum </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.album) </li> </ul> |

### 標籤

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.label </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:**<br/>"Revolver" </li> <li> **說明：**<br/> 記錄標籤的名稱。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. label) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. label) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. label) </li> <li> **資料饋送:** <br/>videoaudiolabel </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.label) </li> </ul> |

### 作者

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.author </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"John Kennedy Toole" </li> <li> **說明：**<br/> 作者的姓名(使用手冊)。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. author) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. author) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. author) </li> <li> **資料饋送:** <br/>videoaudioauthor </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.author) </li> </ul> |

### 電台

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.station </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"NPR" </li> <li> **說明：**<br/> 廣播電台的名稱/ID。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. station) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. station) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. station) </li> <li> **資料饋送:**<br/>videoaudiostation </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.station) </li> </ul> |

### 發行者

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/>media.publisher </li> <li> **必要:**<br/>否 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體開始，媒體關閉 </li> <li> **最小 SDK版本：** 1.5.7 <br/>[媒體系列概述](/help/media-collection-api/mc-api-overview.md) 或 [下載SDK-版本2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **範例值:** <br/>"Random Bauhaus" </li> <li> **說明：**<br/> 音訊內容發行者的名稱。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. publisher) </li> <li> **活動訊號：**<br/> (s：meta：<br/>a. media. publisher) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>eVar </li> <li> **過期時間:**<br/>點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **上下文資料：**<br/> (a. media. publisher) </li> <li> **資料饋送:**<br/>videoaudiopublisher </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.publisher) </li> </ul> |

## 音訊與視訊量度 {#section_3D5F9C555274428AA6030D07596177E9}

### 媒體開始次數

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定</li> <li> **API 索引鍵:**<br/>不適用</li> <li> **類型:**<br/>字串</li> <li> **隨附於：**<br/> 媒體開始</li> <li> **最小 SDK 版本:**&#x200B;任何版本</li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 媒體的載入事件。(觀看者按下&#x200B;_「播放」_&#x200B;按鈕時，即會發生此情形。)即使是前段廣告、緩衝、錯誤等也會計入此值。<br/>**重要:** 如果已設定，則此值只能是 true。If it is not set, no value is returned.  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. view) </li> <li> **活動訊號：**<br/> (s：event：<br/>type= start) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱：**<br/> 媒體開始 </li> <li> **上下文資料：**<br/> (a. media. view) </li> <li> **資料饋送:**<br/>videostart </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.view) </li> </ul> |

### 內容開始

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 會使用第一個媒體影格。If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容開始 </li> <li> **上下文資料：**<br/> (a. media. play) </li> <li> **資料饋送:**<br/>videoplay </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.play) </li> </ul> |

### 內容完成 {#content-complete}

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 已觀看完成的串流。這不一定表示使用者觀看或聆聽整個串流；他們可以跳過先機。這只表示使用者到達串流結尾，100%。<br/>另請參閱 [「工作階段結束」](quality-parameters.md#session-end)<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **活動訊號：**<br/> (s：event：<br/>type= complete) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容完成 </li> <li> **上下文資料：**<br/> (a. media. complete) </li> <li> **資料饋送:**<br/>videocomplete </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.complete) </li> </ul> |

### 內容逗留時間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> 105 </li> <li> **說明：**<br/> 將「播放」主要內容類型的所有事件的事件持續時間(以秒為單位)相加。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容逗留時間 </li> <li> **上下文資料：**<br/> (a. media. TimePlayed) </li> <li> **資料饋送:**<br/>videotime </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.timePlayed) </li> </ul> |

### 媒體逗留時間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> 120 </li> <li> **說明：**<br/> 將所有類型的「播放」(主要和廣告內容)事件的事件持續時間(以秒為單位)相加。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/> 媒體逗留時間 </li> <li> **上下文資料：**<br/> (a. media. totalTimePlayed) </li> <li> **資料饋送:**<br/>videototaltime </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.totalTimePlayed) </li> </ul> |

### 不重複播放時間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> 94 </li> <li> **說明：**<br/> 在工作階段期間播放的內容唯一區段數秒內的值。不包括觀看者向前尋找，並多次觀看同一個內容區段時的播放時間。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>自訂 </li> <li> **上下文資料：**<br/> (a. media. UniqueTimePlayed) </li> <li> **資料饋送:**<br/>videouniquetimeplayed </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. unequeTimePlayed) </li> </ul> |

### 十個進度標記

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 播放磁頭會根據長度傳遞10%的內容標記。此標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>10% 進度標記 </li> <li> **上下文資料：**<br/> (a. media. progress10) </li> <li> **資料饋送:**<br/>videoprogress10 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.progress10) </li> </ul> |

### 25%進度標記

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 播放磁頭會根據內容長度傳遞25%的內容標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>25% 進度標記 </li> <li> **上下文資料：**<br/> (a. media. progress25) </li> <li> **資料饋送:**<br/>videoprogress25 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.progress25) </li> </ul> |

### 50%進度標記

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 播放磁頭會根據內容長度傳遞50%的內容標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>50% 進度標記 </li> <li> **上下文資料：**<br/> (a. media. progress50) </li> <li> **資料饋送:**<br/>videoprogress50 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.progress50) </li> </ul> |

### 月五進度標記

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> **不適用** </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 播放磁頭會根據內容長度傳遞75%的內容標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>75% 進度標記 </li> <li> **上下文資料：**<br/> (a. media. progress75) </li> <li> **資料饋送:**<br/>videoprogress75 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.progress75) </li> </ul> |

### 95%進度標記

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 播放磁頭會根據內容長度傳遞95%的內容標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>95% 進度標記 </li> <li> **上下文資料：**<br/> (a. media. progress95) </li> <li> **資料饋送:**<br/>videoprogress95 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.progress95) </li> </ul> |

### 平均每分鐘觀眾

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>大於或等於 1 </li> <li> **說明：**<br/> 「平均分鐘對象」度量的計算方式為一個特定媒體項目的「總內容逗留時間」，除以其所有播放工作階段的長度： <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **範例值:**<br/>平均每分鐘觀眾 </li> <li> **上下文資料：**<br/> (a. media. averagemugeTeAudience) </li> <li> **資料饋送:**<br/>videoaverageminuteaudience </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 預估資料流量

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值：**<br/> -分鐘播放； <br/>-播放31分鐘； <br/>-播放78分鐘。 </li> <li> **說明：**<br/> 每個個別內容的預計視訊或音訊串流數。播放時間 (內容 + 廣告) 每 30 分鐘這個值就會增加。客戶必須建立自己的處理規則，才能有可用於報告的值。<br/><br/>根據( `ms_s` 或totalTimePlayed= Video總計時間)，每30分鐘計算一次串流，類似： <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>使用自訂處理規則 </li> <li> **預留變數:**<br/>不適用 </li> <li> **報表名稱:**<br/>自訂 </li> <li> **上下文資料：**<br/> (a. media. revestedStreams) </li> <li> **資料饋送:**<br/>不適用 </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a. media. revestedStreams) </li> </ul> |

### 暫停的受影響資料流

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 此值為true或false。It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **活動訊號：**<br/> (s：event：<br/>type= pause) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>暫停的受影響資料流 </li> <li> **上下文資料：**<br/> (a. media. pause) </li> <li> **資料饋送:**<br/>videopause </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.pause) </li> </ul> |

### 暫停事件

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值：**<br/> 2 </li> <li> **說明：**<br/> 此度量的計算方式是暫停工作階段期間發生的暫停期間計數。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **活動訊號：**<br/> (s：event：<br/>type= pause) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>暫停事件 </li> <li> **上下文資料：**<br/> (a. media. pauseCount) </li> <li> **資料饋送:**<br/>videopausecount </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.pauseCount) </li> </ul> |

### 總暫停期間

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>數字 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值：**<br/> 190 </li> <li> **說明：**<br/> 將所有類型的「暫停」類型的持續時間(以秒為單位)相加。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>總暫停期間 </li> <li> **上下文資料：**<br/> (a. media. pauseTime) </li> <li> **資料饋送:**<br/>videopausetime </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.pauseTime) </li> </ul> |

### 內容恢復

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 密鑰:**<br/> **media.resume** </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 每次播放都會計入超過30分鐘緩衝、暫停或失速期間後繼續的每個播放，若此值由VideoInfo TrackPlay上的播放器設定。 <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **活動訊號：**<br/> (s：event：<br/>type= restract) </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容恢復 </li> <li> **上下文資料：**<br/> (a. media. reader) </li> <li> **資料饋送:**<br/>videoresume </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.resume) </li> </ul> |

### 內容區段檢視次數

|   實施   | 網路參數 | 報告 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>自動設定 </li> <li> **API 索引鍵:**<br/>不適用 </li> <li> **類型:**<br/>字串 </li> <li> **隨附於：**<br/> 媒體關閉 </li> <li> **最小 SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>TRUE </li> <li> **說明：**<br/> 主要內容的檢視次數。A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/>不適用 </li> <li> **心率:**<br/>不適用 </li> </ul> | <ul> <li> **可用:**<br/>是 </li> <li> **預留變數:**<br/>事件 </li> <li> **報表名稱:**<br/>內容區段檢視次數 </li> <li> **上下文資料：**<br/> (a. media. segmentView) </li> <li> **資料饋送:**<br/>videosegmentviews </li> <li> **Audience Manager：**<br/> (c_ contextData.<br/>a.media.segmentView) </li> </ul> |

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

