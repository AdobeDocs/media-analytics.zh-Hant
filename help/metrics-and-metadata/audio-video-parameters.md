---
title: 音訊和視訊參數
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 82b38f7870b6f890aaa812de30fa2d02d4f3ba8a
workflow-type: tm+mt
source-wordcount: '6234'
ht-degree: 99%

---


# 音訊和視訊參數{#audio-and-video-parameters}

>[!IMPORTANT]
>
>在 2019 年 2 月 7 日，Adobe Analytics for Video and Audio 發佈了量度名稱變更。<i>媒體起始</i>將更名為<i>媒體開始次數</i>。做出這項變更是為了反映量度和報告的業界標準，並讓量度在報告中易於識別。

>[!NOTE]
>
>從 2018 年 9 月 13 日開始，我們變更了某些維度、量度與報表的標籤，以便交叉追蹤 Video Analytics 與 Audio Analytics 的內容。變更的標籤包括：*視訊起始*&#x200B;變更為&#x200B;*媒體起始*、*視訊長度*&#x200B;變更為&#x200B;*內容長度*、*視訊名稱*&#x200B;變更為&#x200B;*內容名稱*。Reports and Analytics 中的視訊報表已全數更新，捨棄「視訊」一名而改用「媒體」。標籤變更並未改變資料收集或歷史資料。如果您要在 Report Builder 或其他任何受到前述變更影響的外部自動化資料提取中使用這些標籤，請多加留意。

本主題介紹音訊與視訊內容資料清單，包含 Adobe 透過解決方案變數收集的內容資料值。

表格資料說明:

* **實作：**&#x200B;實作數值和需求的資訊
   * *索引鍵* - 在您的應用程式中手動設定，或由 Adobe Media SDK 自動設定的變數。
   * *必要* - 指出基本音訊與視訊追蹤是否需要參數。
   * *類型* - 指明預計設定的變數類型 (字串或數字)。
   * *「伴隨傳送」*- 指出資料傳送的時間:*「媒體開始」*&#x200B;為媒體開始時傳送的分析呼叫、*「廣告開始」*&#x200B;為廣告開始時傳送的分析呼叫等等；*「關閉」*&#x200B;呼叫為媒體工作階段結束或廣告、章節等項目結束時，直接從心率伺服器傳送到分析伺服器的已編譯分析呼叫。網路封包呼叫中使用無法使用關閉呼叫。
   * *最低SDK 版本* - 指出您存取參數所需的 SDK 版本。
   * *範例值* - 提供常見的變數使用方法範例。
* **網路參數：**&#x200B;顯示傳遞至 Adobe Analytics 或心率伺服器的數值。本欄顯示可於網路呼叫中看到，且由 Adobe Media SDK 產生的參數名稱。
* **報表：**&#x200B;關於如何檢視和分析音訊與視訊資料的資訊。
   * *可用* - 指出資料是否已由報表預設提供 (*是*)，或是需要自行設定 (*自訂*)
   * *保留變數* - 指出資料在保留變數中是否被當作事件、eVar、prop 或分類擷取。
   * *到期* - 指示資料是否會在每次點擊或每次造訪後到期。
   * *報表名稱* - 適用於變數的 Adobe Aanlytics 報表名稱
   * *內容資料* - 傳遞至報表伺服器以及用於處理規則的 Adobe Aanlytics 內容資料名稱。
   * *資料摘要* - 可在 Clickstream 或 Live Stream 資料摘要中找到的變數欄名稱
   * *Audience Manager* - Adobe Audience Manager 中的特徵名稱

>[!IMPORTANT]
>
>請勿變更下列任何變數的分類名稱，其說明以「分類」形式顯示於「報表/保留變數」下方。\
>為媒體追蹤啟用報表套裝時，系統會定義媒體分類。Adobe 有時會新增屬性，而發生這種情形時，客戶必須重新啟用其報表套裝才能存取新的媒體屬性。在更新程序期間，Adobe 會檢查變數名稱，藉此決定是否啟用分類。如果有任何變數名稱遺失，Adobe 會再次新增遺失的項目。

## 核心串流媒體資料{#core-audio-and-video-data}

### 資料流類型 {#stream-type}

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.streamType </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 2.2 <br/><br/>可在[媒體收集 API 概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li>  <li> **範例值:**<br/> &quot;video&quot; </li> <li> **說明:**<br/> 識別資料流類型。有效值為 &quot;audio&quot;、&quot;video&quot; 及 &quot;&quot;。<br/><br/>[報表區段](/help/metrics-and-metadata/segments.md): <br/><br/>媒體資料流類型: 全部 - <br/>劃分所有媒體資料流資料；規則: 內容 (ID) 存在 <br/><br/>媒體資料流類型: 音訊 - <br/>劃分所有音訊資料流資料；規則: 內容 (ID) 存在且媒體資料流類型 = 音訊 <br/><br/>媒體資料流類型 :「視訊」- <br/>劃分所有視訊資料流資料；規則: 內容 (ID) 存在且媒體資料流類型! = 音訊 <br/><br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;造訪時 </li> <li> **報表名稱:**<br/>&#x200B;內容 </li> <li> **內容資料:**<br/> (a.media.streamType) </li> <li> **資料饋送:**<br/> videostreamtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.id </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> &quot;4586695ABC&quot; </li> <li>**說明:**<br/> 內容的「內容 ID」，可用來繫結其他業界 / CMS ID，等同於 `s:asset:video_id.` 的最後一個值 </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **心率:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;造訪時 </li> <li> **報表名稱:**<br/>&#x200B;內容 </li> <li> **內容資料:**<br/> (a.media.name) </li> <li> **資料饋送:**<br/>&#x200B;影片 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.length </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> VOD: 128；即時: 86400；線性: 1800。 </li><li> **說明:**<br/> 按一下長度/執行階段 - 這是被使用內容的最大長度 (或持續時間) (以秒為單位)。其等同於來自「主要」類型事件的 `l:asset:length` 的最後一個值。<br/>如果未設定 `l:asset:length`，則使用 `l:asset:duration` 的最後一個值。<br/>在報表中，以「視訊長度」為其分類，以「內容長度 (變數)」為 eVAR。<br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。<br/>1.5.1 之前的版本是 `l:asset:duration`；在 1.5.1 之後則為 `l:asset:length.` <br/> **發行日期: 2018 年 9 月 13 日** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **心率:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> 內容長度 (變數) </li> <li> **內容資料:**<br/> (a.media.length) </li> <li> **資料饋送:**<br/> videolength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/>  [長度](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.length </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> VOD: 128；即時: 86400；線性: 1800。 </li> <li> **說明:**<br/> 按一下長度/執行階段 - 這是被使用內容的最大長度 (或持續時間) (以秒為單位)。其等同於來自「主要」類型事件的 `l:asset:length` 的最後一個值。如果未設定 `l:asset:length`，則使用 `l:asset:duration` 的最後一個值。在報表中，以「視訊長度」為其分類，以「內容長度 (變數)」為 eVAR。<br/> **重要:** 此屬性用於運算多個量度，例如進度追蹤量度以及「平均每分鐘觀眾」。如果未設定或是值並未大於零，則無法使用這些量度。如果是持續時間不明的即時媒體，則以 86400 的值為預設。1.5.1 之前的版本是 `l:asset:duration`；在 1.5.1 之後則為 `l:asset:length.`<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **心率:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> 視訊長度 </li> <li> **內容資料:**<br/> (a.media.length) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.contentType </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;限制字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> &quot;vod&quot; </li> <li> **說明:**<br/> 各種&#x200B;**資料流類型**&#x200B;的可用值: <br/> _音訊:_ &quot;song&quot;、&quot;podcast&quot;、&quot;audiobook&quot;、&quot;radio&quot; <br/> _視訊:_「VoD」、「即時」、「線性」、「UGC」、「DVoD」<br/>客戶能提供該參數的自訂值。這等於 `s:stream:type.` 如果未設定，就等於 `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **心率:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;內容類型 </li> <li> **內容資料:**<br/> (a.contentType) </li> <li> **資料饋送:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;取自後端 </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.8 </li> <li> **範例值:**<br/> 1482236761294786918253 </li> <li> **說明:**<br/> 此可識別個別播放所獨有的內容資料流的例項。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **心率:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **可用性:**<br/>&#x200B;使用處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.vsid) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### 下載的媒體標幟

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> `config.downloadedcontent` </li> <li> **API 索引鍵:**<br/>&#x200B;取自後端 </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/> 布林值 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** <br/>Launch Android 和 iOS 擴充功能 1.1.0 版 </li> <li> **範例值:**<br/> true </li> <li> **說明:**<br/> 在因播放下載的內容媒體工作階段而產生點擊時，則設為 true。未播放下載的內容時，則不存在。<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.downloaded) </li> <li> **心率:**<br/> (s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.downloaded) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### 內容播放器名稱

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/> media.playerName </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>「Brightcove」 </li> <li> **說明:**<br/> 播放器名稱。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **心率:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;內容播放器名稱 </li> <li> **內容資料:**<br/> (a.media.playerName) </li> <li> **資料饋送:**<br/> ideoplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### 內容頻道

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/> media.channel </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> &quot;Sports&quot; </li> <li> **說明:**<br/> 發佈的站台/頻道、或播放內容的位置。此處接受的任何字串值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **心率:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;內容管道 </li> <li> **內容資料:**<br/> (a.media.channel) </li> <li> **資料饋送:**<br/> videochannel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### 內容區段

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;是 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>「0-10」 </li> <li> **說明:**<br/> 說明已檢視部分內容的間隔 (以分鐘計)。此區段的計算方式為播放工作階段期間播放點值的最大值與最小值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;內容區段 </li> <li> **內容資料:**<br/> (a.media.segment) </li> <li> **資料饋送:**<br/> videosegment </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### 內容名稱 (變數)

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API 索引鍵:**<br/> media.name </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.1 </li> <li> **範例值:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **說明:**<br/> 這是內容的「易記」(人類看得懂的) 名稱，等於 `s:asset:name.`<br/> 的最後一個值在報表中，以「視訊名稱」為其分類，以「內容名稱 (變數)」為 eVAR。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **心率:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> 內容名稱 (變數) </li> <li> **內容資料:**<br/> (a.media.friendlyName) </li> <li> **資料饋送:**<br/> videoname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

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
| <ul> <li> **SDK 索引鍵:**<br/>  [名稱](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/> media.name </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.1 </li> <li> **範例值:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **說明:**<br/> 這是內容的「易記」(人類看得懂的) 名稱，等於 `s:asset:name.` 的最後一個值<br/>在報表中，以「視訊名稱」為其分類，以「內容名稱 (變數)」為 eVAR。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>好記名稱) </li> <li> **心率:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> 視訊名稱 </li> <li> **內容資料:**<br/> (a.media.friendlyName) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### 視訊路徑

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> &quot;4586695ABC&quot; </li> <li> **說明:**<br/> 提供可在網站及/或應用程式上追蹤檢視器路徑的功能，可查看其觀看特定視訊所使用的路徑。任何整數和/或字母的組合。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **心率:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **保留變數:**<br/> prop </li> <li> **報表名稱:**<br/>&#x200B;視訊路徑 </li> <li> **內容資料:**<br/> (a.media.name) </li> <li> **資料饋送:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK 版本

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 索引鍵:**<br/> media.sdkVersion </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> &quot;2.62.0_release&quot; </li> <li> **說明:**<br/> 播放器使用的 SDK 版本。您可以採用播放器適用的自訂值。<br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **心率:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.sdkVersion) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 版本

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **說明:**<br/> 追蹤工作階段所使用的媒體 SDK 版本。<br/><br/>客戶必須建立自己的處理規則，才能有可用於報表的值。<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **心率:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.vhlVersion) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 標準串流媒體中繼資料{#standard-audio-and-video-metadata}

### 節目

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> SHOW </li> <li> **API 索引鍵:**<br/> media.show </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> &quot;Modern Family&quot;、&quot;The Last Dance&quot;、&quot;New Girl&quot; </li> <li> **說明:**<br/> 影集/系列名稱 <br/>僅限該影集為一系列當中的一部分時，才需要提供「影集名稱」。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;節目 </li> <li> **內容資料:**<br/> (a.media.show) </li> <li> **資料饋送:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### 資料流格式

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> STREAM_FORMAT </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> &quot;Live&quot; </li> <li> **說明:**<br/> 串流格式 (即時、VOD、線性)。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.format) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### 季數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> SEASON </li> <li> **API 索引鍵:**<br/> media.season </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「2」 </li> <li> **說明:**<br/>&#x200B;該節目所隸屬的季數。僅限該節目為一系列當中的一部分時，才需要提供「季系列」。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.season) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;季數 </li> <li> **內容資料:**<br/> (a.media.season) </li> <li> **資料饋送:**<br/> videoseason </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.season) </li> </ul> |

### 集數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> EPISODE </li> <li> **API 索引鍵:**<br/> media.episode </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「13」 </li> <li> **說明:**<br/> 代表集數的數目。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;集數 </li> <li> **內容資料:**<br/> (a.media.episode) </li> <li> **資料饋送:**<br/> videoepisode </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### 資產 ID

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> ASSET_ID </li> <li> **API 索引鍵:**<br/> media.assetId </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「89745363」 </li> <li> **說明:**<br/> 這是媒體資產內容的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;資產 ID </li> <li> **內容資料:**<br/> (a.media.asset) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### 類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> GENRE </li> <li> **API 索引鍵:**<br/> media.genre </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「Drama」、「Comedy」 </li> <li> **說明:**<br/> 內容的類型或分組如內容製作程式所定義。應在實施變數時以逗號分隔這些值。在報表中，eVar 清單會將每個值拆分到條列項目中，每個條列項目接受同樣的量度加權。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **保留變數:**<br/> eVar 清單 </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;類型 </li> <li> **內容資料:**<br/> (a.media.genre) </li> <li> **資料饋送:**<br/> videogenre </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### 首播日期

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> FIRST_AIR_DATE </li> <li> **API 索引鍵:**<br/> media.firstAirDate </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「2016-01-25」 </li> <li> **說明:**<br/> 內容在電視上的首播日期。任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> 首播日期 </li> <li> **內容資料:**<br/> (a.media.airDate) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### 首次數位化日期

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> FIRST_DIGITAL_DATE </li> <li> **API 索引鍵:**<br/> media.firstDigitalDate </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「2016-01-25」 </li> <li> **說明:**<br/> 內容在任何數位頻道或平台上的首播日期。任何日期格式皆可接受，不過 Adobe 建議: YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/> 首次數位化日期 </li> <li> **內容資料:**<br/> (a.media.digitalDate) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### 內容評等

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> RATING </li> <li> **API 索引鍵:**<br/> media.rating </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> TVY、TVG、TVPG、TVMA </li> <li> **說明:**<br/> 依美國電視分級制度 (TV Parental Guidelines) 的定義進行分級。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/>&#x200B;內容分級 </li> <li> **內容資料:**<br/> (a.media.rating) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### 創作者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> ORIGINATOR </li> <li> **API 索引鍵:**<br/> media.originator </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「Warner Brothers」、「Sony」、「Disney」 </li> <li> **說明:**<br/> 內容的建立者。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;分類 </li> <li> **報表名稱:**<br/> 創作者 </li> <li> **內容資料:**<br/> (a.media.originator) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### 網路

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> NETWORK </li> <li> **API 索引鍵:**<br/> media.network </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「Fox」、「Bravo」、「ESPN」等 </li> <li> **說明:**<br/> 網路/頻道名稱。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;網路 </li> <li> **內容資料:**<br/> (a.media.network) </li> <li> **資料饋送:**<br/> videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### 節目類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> SHOW_TYPE </li> <li> **API 索引鍵:**<br/> media.showType </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「0」= 全集；「1」= 預覽/預告；「2」= 片段；「3」= 其他。 </li> <li> **說明:**<br/> 內容的類型，以介於 0 和 3 之間的整數表示。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;節目類型 </li> <li> **內容資料:**<br/> (a.media.type) </li> <li> **資料饋送:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> MVPD </li> <li> **API 索引鍵:**<br/> media.pass.mvpd </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「Comcast」、「DirecTV」、「Dish」 </li> <li> **說明:**<br/> 透過 Adobe 驗證提供的 MVPD。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/> MVPD </li> <li> **內容資料:**<br/> (a.media.pass.mvpd) </li> <li> **資料饋送:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 已驗證

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> AUTHORIZED </li> <li> **API 索引鍵:**<br/> media.pass.auth </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「TRUE」 </li> <li> **說明:**<br/> 使用者已透過 Adobe 驗證取得授權。<br/>**重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱名稱:**<br/>&#x200B;已授權 </li> <li> **內容資料:**<br/> (a.media.pass.auth) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 時段

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> DAY_PART </li> <li> **API 索引鍵:**<br/> media.dayPart </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/> </li> <li> **說明:**<br/> 定義內容播出或播放當天時間的屬性。可由客戶按照需求設定任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;時段 </li> <li> **內容資料:**<br/> (a.media.dayPart) </li> <li> **資料饋送:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### 媒體摘要類型

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> FEED </li> <li> **API 索引鍵:**<br/> media.feed </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 </li> <li> **範例值:**<br/>「East-HD」、「West-HD」、「East-SD」 </li> <li> **說明:**<br/> 輸出類型。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報表名稱:**<br/>&#x200B;媒體摘要類型 </li> <li> **內容資料:**<br/> (a.media.feed) </li> <li> **資料饋送:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### 藝人

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.artist </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/> &quot;The Beatles&quot; </li> <li> **說明:**<br/> 藝人姓名。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.artist) </li> <li> **資料饋送:**<br/> videoaudioartist </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artist) </li> </ul> |

### 專輯

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.album </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/>&quot;Revolver&quot; </li> <li> **說明:**<br/> 專輯名稱。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.album) </li> <li> **資料饋送:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### 標籤

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.label </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/>&quot;Revolver&quot; </li> <li> **說明:**<br/> 唱片公司的名稱。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.label) </li> <li> **資料饋送:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### 作者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.author </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **說明:**<br/> 作者姓名 (有聲書)。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.author) </li> <li> **資料饋送:**<br/> videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### 電台

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.station </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/> &quot;NPR&quot; </li> <li> **說明:**<br/> 廣播電台的名稱 / ID。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.station) </li> <li> **資料饋送:**<br/> videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### 發行者

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> </li> <li> **API 索引鍵:**<br/> media.publisher </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體開始、媒體關閉 </li> <li> **最小SDK 版本:** 1.5.7 <br/>可在[媒體收集概述](/help/media-collection-api/mc-api-overview.md)或[下載 SDK - 2.2 版](/help/sdk-implement/download-sdks.md)中取得。  </li> <li> **範例值:**<br/> &quot;Random Bauhaus&quot; </li> <li> **說明:**<br/> 音訊內容發行者姓名。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **心率:**<br/> (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;點擊時 </li> <li> **報告名稱:**<br/> </li> <li> **內容資料:**<br/> (a.media.publisher) </li> <li> **資料饋送:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## 串流媒體量度{#audio-and-video-metrics}

### 媒體開始次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定</li> <li> **API 索引鍵:**<br/>&#x200B;不適用</li> <li> **類型:**<br/>&#x200B;字串</li> <li> **伴隨傳送:**<br/> 媒體開始</li> <li> **最小SDK 版本:**&#x200B;任何版本</li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 為該媒體載入事件。(觀看者按下&#x200B;_「播放」_&#x200B;按鈕時，即會發生此情形。)即使是前段廣告、緩衝、錯誤等也會計入此值。<br/>**重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **心率:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 媒體開始 </li> <li> **內容資料:**<br/> (a.media.view) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### 內容開始

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 使用媒體的第一個時間格。如果使用者在廣告、緩衝等期間中斷，就沒有「內容開始」事件。<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;內容開始 </li> <li> **內容資料:**<br/> (a.media.play) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### 內容完成 {#content-complete}

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 觀看至結束的資料流。這並不代表使用者已看完或聽完整個資料流，他們有可能提前略過。這只表示使用者達到資料流結尾 100% 的部分。<br/>另請參閱[工作階段結束](quality-parameters.md#session-end) <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;內容完成 </li> <li> **內容資料:**<br/> (a.media.complete) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### 內容逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 105 </li> <li> **說明:**<br/> 主要內容中屬於「播放」類型之所有事件持續時間的總和 (以秒為單位)。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。 <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;內容逗留時間 </li> <li> **內容資料:**<br/> (a.media.timePlayed) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### 媒體逗留時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 120 </li> <li> **說明:**<br/> 主要內容和廣告內容中，屬於「播放」類型之所有事件持續時間的總和 (以秒為單位)。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 媒體逗留時間 </li> <li> **內容資料:**<br/> (a.media.totalTimePlayed) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### 不重複播放時間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 94 </li> <li> **說明:**<br/> 在工作階段期間，播放不重複之內容區段的值 (以秒為單位)。不包括觀看者向前尋找，並多次觀看同一個內容區段時的播放時間。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。  <br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.uniqueTimePlayed) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10% 進度標記

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 根據長度，播放點超過內容的 10% 標記。此標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。        <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 10% 進度標記 </li> <li> **內容資料:**<br/> (a.media.progress10) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25% 進度標記

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 根據內容長度，播放點超過內容的 25% 標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。         <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 25% 進度標記 </li> <li> **內容資料:**<br/> (a.media.progress25) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50% 進度標記

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 根據內容長度，播放點超過內容的 50% 標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。         <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 50% 進度標記 </li> <li> **內容資料:**<br/> (a.media.progress50) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75% 進度標記

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 密鑰:**<br/> **不適用** </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 根據內容長度，播放點超過內容的 75% 標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。         <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 75% 進度標記 </li> <li> **內容資料:**<br/> (a.media.progress75) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95% 進度標記

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 根據內容長度，播放點超過內容的 95% 標記。標記只會計算 1 次，即使回頭搜尋也不會重覆計入。如果往前搜尋，則略過的標記並不會計入。         <br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/> 95% 進度標記 </li> <li> **內容資料:**<br/> (a.media.progress95) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### 平均每分鐘觀眾

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/>&#x200B;大於或等於 1 </li> <li> **說明:**<br/>「平均每分鐘觀眾」量度的計算方式為特定媒體項目的「內容總逗留時間」除以所有播放工作階段的長度: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **範例值:**<br/>&#x200B;平均每分鐘觀眾 </li> <li> **內容資料:**<br/> (a.media.averageMinuteAudience) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 上次通話後經過秒數

|   實作   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 600</li> <li> **說明：**<br/>&#x200B;如果資料流是以完整事件或結束事件關閉，則上次呼叫量度後的秒數為 0；如果因逾時而關閉，則通常為 600。此量度沒有解決方案變數和自動處理規則，因此您必須建立自訂處理規則才能儲存。</li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;不適用 </li> <li> **內容資料：**<br/>(a.media.secondsSinceLastCall) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> </ul> |

### 同盟資料

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/> 布林值 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> true  </li> <li> **說明:**<br/> 若點擊已建立同盟，則設為 true (也就是說，客戶收到的點擊是做為同盟資料共用的一部分，而不是客戶自己的實施)。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;不適用 </li> <li> **內容資料:**<br/> (a.media.federated) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### 預估資料流量

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 1 - 播放 19 分鐘；<br/>2 - 播放 31 分鐘；<br/>3 - 播放 78 分鐘。 </li> <li> **說明:**<br/> 每個單獨內容的預估視訊或音訊資料流量。播放時間 (內容 + 廣告) 每 30 分鐘這個值就會增加。客戶必須建立自己的處理規則，才能有可用於報告的值。<br/><br/>每隔 30 分鐘就會根據 `ms_s` (或 totalTimePlayed = 視訊總時間) 計算一次資料流量，計算方式與以下類似: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **內容資料:**<br/> (a.media.estimatedStreams) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### 暫停的受影響資料流

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 此值不是 true 就是 false。如果在播放單一媒體項目期間發生一或多次暫停就是 true。<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;暫停的受影響資料流 </li> <li> **內容資料:**<br/> (a.media.pause) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### 暫停事件

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/> 2 </li> <li> **說明:**<br/> 此度量的計算方式為播放工作階段期間發生的暫停期間的計數。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;暫停事件 </li> <li> **內容資料:**<br/> (a.media.pauseCount) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 總暫停期間

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/> 190 </li> <li> **說明:**<br/> 屬於「暫停」類型之所有事件持續時間的總和 (以秒為單位)。該值在 Analysis Workspace 與 Reports &amp; Analytics 中將以時間格式 (HH:MM:SS) 顯示。在資料摘要、Data Warehouse 及報表 API 中，該值將以秒數顯示。<br/> **發行日期: 2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;總暫停期間 </li> <li> **內容資料:**<br/> (a.media.pauseTime) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### 內容恢復

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 密鑰:**<br/> **media.resume** </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:** 1.5.6 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 在超過 30 分鐘的緩衝、暫停或停頓期間之後繼續的每次播放，或此值由播放器在 VideoInfo trackPlay 上設定，便會計入一次繼續。<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;內容恢復 </li> <li> **內容資料:**<br/> (a.media.resume) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### 內容區段檢視次數

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/>&#x200B;自動設定 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;字串 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> TRUE </li> <li> **說明:**<br/> 主要內容的檢視次數。至少檢視了一個時間格時，會計入一次內容區段檢視。<br/> **重要:** 如果已設定，則此值只能是 true。如果尚未設定，則不會傳回任何值。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/>&#x200B;事件 </li> <li> **報表名稱:**<br/>&#x200B;內容區段檢視次數 </li> <li> **內容資料:**<br/> (a.media.segmentView) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### 廣告計數

|   實作   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> 不適用 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 2 </li> <li> **說明：**<br/> 媒體工作階段期間開始的廣告數。    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **上下文資料：**<br/> (a.media.adCount) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### 章節計數

|   實作   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> 不適用 </li> <li> **API 索引鍵:**<br/>&#x200B;不適用 </li> <li> **類型:**<br/>&#x200B;數字 </li> <li> **伴隨傳送:**<br/> 媒體關閉 </li> <li> **最小SDK 版本:**&#x200B;任何版本 </li> <li> **範例值:**<br/> 2 </li> <li> **說明：**<br/> 媒體作業期間開始的章節數。    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>&#x200B;不適用 </li> <li> **心率:**<br/>&#x200B;不適用 </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;使用自訂處理規則 </li> <li> **預留變數:**<br/>&#x200B;不適用 </li> <li> **報表名稱:**<br/>&#x200B;自訂 </li> <li> **上下文資料：**<br/> (a.media.chapterCount) </li> <li> **資料饋送:**<br/>&#x200B;不適用 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |


## 加州消費者隱私法 (CCPA) 參數 {#ccpa-params}

### 選擇退出伺服器端轉送

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> 不適用 </li> <li> **API 索引鍵:**<br/> analytics.optOutServerSideForwarding </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/> 布林值 </li> <li> **伴隨傳送:**<br/> 媒體開始 </li> <li> **最小SDK 版本:** 不適用 </li> <li> **範例值:**<br/> true </li> <li>**說明:**<br/> 若使用者已選擇退出其在 Adobe Analytics 與其他 Experience Cloud 解決方案 (例如 Audience Manager) 之間共用的資料，則設為 true。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **心率:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;造訪時 </li> <li> **報表名稱:**<br/>&#x200B;內容 </li> <li> **內容資料:**<br/> 不適用 </li> <li> **資料饋送:**<br/>&#x200B;影片 </li> <li> **Audience Manager:**<br/> 不適用 </li> </ul> |

### 選擇退出共用

|   實施   | 網路參數 | 報表 |
| --- | --- | --- |
| <ul> <li> **SDK 索引鍵:**<br/> 不適用 </li> <li> **API 索引鍵:**<br/> analytics.optOutShare </li> <li> **必要:**<br/>&#x200B;否 </li> <li> **類型:**<br/> 布林值 </li> <li> **伴隨傳送:**<br/> 媒體開始 </li> <li> **最小SDK 版本:** 不適用 </li> <li> **範例值:**<br/> true </li> <li>**說明:**<br/> 若使用者已選擇退出為其資料建立同盟 (例如與其他 Adobe Analytics 用戶端建立同盟)，則設為 true。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **心率:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **可用:**<br/>&#x200B;是 </li> <li> **預留變數:**<br/> eVar </li> <li> **過期時間:**<br/>&#x200B;造訪時 </li> <li> **報表名稱:**<br/>&#x200B;內容 </li> <li> **內容資料:**<br/> 不適用 </li> <li> **資料饋送:**<br/>&#x200B;影片 </li> <li> **Audience Manager:**<br/> 不適用 </li> </ul> |

## 相關 API {#section_Related_APIs}

### createMediaObject API {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig API {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
