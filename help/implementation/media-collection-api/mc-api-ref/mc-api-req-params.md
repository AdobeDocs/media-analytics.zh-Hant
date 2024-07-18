---
title: 串流媒體收集 API - 要求參數
description: 「什麼是 Media Collection API 要求參數、要求索引鍵和說明。」
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 100%

---

# 要求參數{#request-parameters}

## Analytics 資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | 字串 | `sessionStart` | Adobe Analytics 伺服器的 URL |
| `analytics.reportSuite` | Y | 字串 | `sessionStart` | 識別 Analytics 報表資料的 ID |
| `analytics.enableSSL` | N | 布林值 | `sessionStart` | 是否啟用 SSL (True 或 False) |
| `analytics.visitorId` | N | 字串 | `sessionStart` | Adobe 訪客 ID 是可用於多款 Adobe 應用程式的自訂 ID。心率 `visitorId` 等於 Analytics `VID.` |

## 訪客資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | 字串 | `sessionStart` | Experience Cloud 組織 ID，能在 Adobe Experience Cloud 生態系統中識別您的組織 |
| `visitor.marketingCloudUserId` | N | 字串 | `sessionStart` | 這是 Experience Cloud 使用者 ID (ECID)。在大多數案例中，這是識別使用者時應使用的 ID。心率 `marketingCloudUserId` 等於 Adobe Analytics 中的 `MID`。此參數就技術上而言雖然並非必要，但在存取 Experience Cloud 應用程式系列時則需使用此參數。 |
| `visitor.aamLocationHint` | N | 整數 | `sessionStart` | 提供 Adobe Audience Manager Edge 資料 - 如果未輸入值，則為空值。 |
| `appInstallationId` | N | 字串 | `sessionStart` | 唯一識別應用程式和裝置的 appInstallationId |

## 內容資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | 字串 | `sessionStart` | 內容的唯一識別碼 |
| `media.name` | N | 字串 | `sessionStart` | 內容的人類可讀名稱 |
| `media.length` | Y | 數字 | `sessionStart` | 內容長度 (秒) |
| `media.contentType` | Y | 字串 | `sessionStart` | 資料流的格式 (可以是任何字串；幾個建議的值包括「即時」、「VOD」或「線性」) |
| `media.playerName` | Y | 字串 | `sessionStart` | 負責轉譯內容之播放器的名稱 |
| `media.channel` | Y | 字串 | `sessionStart` | 內容發佈的管道。可以是行動應用程式名稱或網站名稱、屬性名稱 |
| `media.resume` | N | 布林值 | `sessionStart` | 指出使用者是否正在繼續先前的工作階段 (相對於開始新的工作階段) |
| `media.sdkVersion` | N | 字串 | `sessionStart` | 播放器使用的 SDK 版本 |

## 內容標準中繼資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | 字串 | `sessionStart` | 串流格式，例如「HD」 |
| `media.show` | N | 字串 | `sessionStart` | 節目或影集名稱 |
| `media.season` | N | 字串 | `sessionStart` | 節目或影集隸屬的季數 |
| `media.episode` | N | 字串 | `sessionStart` | 集數 |
| `media.assetId` | N | 字串 | `sessionStart` | 視訊資產的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。 |
| `media.genre` | N | 字串 | `sessionStart` | 內容製作人定義的內容類型 |
| `media.firstAirDate` | N | 字串 | `sessionStart` | 內容在電視上的首播日期 |
| `media.firstDigitalDate` | N | 字串 | `sessionStart` | 內容在任何數位平台上的首播日期 |
| `media.rating` | N | 字串 | `sessionStart` | 依美國電視分級制度 (TV Parental Guidelines) 的定義進行分級 |
| `media.originator` | N | 字串 | `sessionStart` | 內容的建立者 |
| `media.network` | N | 字串 | `sessionStart` | 網路 / 頻道名稱 |
| `media.showType` | N | 字串 | `sessionStart` | 內容的類型，以 0 到 3 的整數來表示： <ul> <li>0 – 全集 </li> <li>1 – 預覽 </li> <li>2 – 片段 </li> <li>3 – 其他 </li> </ul> |
| `media.adLoad` | N | 字串 | `sessionStart` | 載入的廣告類型 |
| `media.pass.mvpd` | N | 字串 | `sessionStart` | Adobe 驗證提供的 MVPD |
| `media.pass.auth` | N | 字串 | `sessionStart` | 指出使用者已獲得 Adobe 驗證授權 (若有設定，只能為 True) |
| `media.dayPart` | N | 字串 | `sessionStart` | 內容播出當天的時間 |
| `media.feed` | N | 字串 | `sessionStart` | 摘要類型，如 &quot;West-HD&quot; |

## 廣告資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | 字串 | `adBreakStart` | 廣告插播的易記名稱 |
| `media.ad.podIndex` | Y | 整數 | `adBreakStart` | 視訊中的廣告 Pod 索引 |
| `media.ad.podSecond` | Y | 數字 | `adBreakStart` | Pod 開始的秒數 |
| `media.ad.podPosition` | Y | 整數 | `adStart` | 廣告插播中的廣告索引，從 1 開始 |
| `media.ad.name` | N | 字串 | `adStart` | 廣告的易記名稱 |
| `media.ad.id` | Y | 字串 | `adStart` | 廣告名稱 |
| `media.ad.length` | Y | 數字 | `adStart` | 視訊廣告長度 (以秒為單位) |
| `media.ad.playerName` | Y | 字串 | `adStart` | 負責轉譯廣告之播放器的名稱 |

## 廣告標準中繼資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | 字串 | `adStart` | 廣告中精選產品的公司或品牌 |
| `media.ad.campaignId` | N | 字串 | `adStart` | 廣告促銷活動 ID |
| `media.ad.creativeId` | N | 字串 | `adStart` | 廣告創意 ID |
| `media.ad.siteId` | N | 字串 | `adStart` | 廣告網站 ID |
| `media.ad.creativeURL` | N | 字串 | `adStart` | 廣告創意的 URL |
| `media.ad.placementId` | N | 字串 | `adStart` | 廣告版位 ID |

## 章節資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | 整數 | `chapterStart` | 識別章節在內容中的位置 |
| `media.chapter.offset` | Y | 數字 | `chapterStart` | 章節開始播放的秒數 |
| `media.chapter.length` | Y | 數字 | `chapterStart` | 章節的長度 (以秒為單位) |
| `media.chapter.friendlyName` | N | 字串 | `chapterStart` | 章節的人類易記名稱 |

## 品質資料

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | 整數 | 任何 | 平均位元速率 (以每秒位元數為單位)。平均位元速率的計算方式，為播放作業工作階段期間發生、與播放期間相關的所有位元速率值的加權平均。 |
| `media.qoe.droppedFrames` | N | 整數 | 任何 | 資料流掉格的數量 |
| `media.qoe.framesPerSecond` | N | 整數 | 任何 | 每秒時間格數量 |
| `media.qoe.timeToStart` | N | 整數 | 任何 | 從使用者點擊播放到內容載入並開始播放之間的時間量 (以毫秒為單位) |

## 加州消費者隱私法 (CCPA) 參數 {#ccpa-params}

| 要求索引鍵 | 必填 | 要求類型索引鍵 | 設定於... |  說明 |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | 布林值 | `sessionStart` | 若使用者已選擇退出其在 Adobe Analytics 與其他 Experience Cloud 解決方案 (例如 Audience Manager) 之間共用的資料，則設為 true |
| `analytics.optOutShare` | N | 布林值 | `sessionStart` | 若使用者已選擇退出為其資料建立同盟 (例如與其他 Adobe Analytics 用戶端建立同盟)，則設為 true。 |

## 其他詳細資料 {#additional-details}

### visitor.marketingCloudUserId

使用以下索引鍵將 Experience Cloud 使用者 ID (亦稱為 `MID` 或 `MCID`) 加入 `params` 對應，再透過 `sessionStart` 呼叫予以傳遞：**visitor.marketingCloudUserId**。如果您已經與 Experience Cloud 產品整合，而且已取得 MCID，這項功能將會非常實用。

>[!NOTE]
>
>Media Analytics (MA) 已與 Experience Cloud 應用程式系列 (Adobe Analytics、Audience Manager、Target 等) 整合。若要存取這些應用程式，您需要 Experience Cloud ID。_在大多數案例中，您應在識別使用者時使用 ECID。_

### appInstallationId

* **如果您&#x200B;*未*傳遞 `appInstallationId` 值 -** MA 後端將不再產生 MCID，而是會仰賴 Adobe Analytics 來產生。Adobe 建議您盡可能傳送 MCID 或 `appInstallationId` (連同目前仍為必要項目的 `marketingCloudOrgId`)，讓媒體收集 API 在每次呼叫時產生 MCID 並予以傳送。

* **如果您&#x200B;*會*傳遞 `appInstallationId` 值 -** 如果您會傳遞 `appInstallationId` 的值和 (必要的) `marketingCloudOrgId` 參數，則 MA 後端&#x200B;*能*&#x200B;產生 MCID。如果您自行傳遞 `appInstallationId`，必須將其值保留在用戶端上。該值必須供裝置上的應用程式專用，而且只要您未重新安裝應用程式，該值就必須存在。

>[!NOTE]
>
>唯一識別應用程式&#x200B;*和裝置*&#x200B;的 `appInstallationId`。每部裝置上的每個應用程式都必須有專屬的值。也就是說，假設有兩位使用者在兩部相異裝置上使用同一款應用程式的相同版本，他們必須分別傳送不同 (唯一) 的 `appInstallationId`。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

除了是在未提供 MCID 時用來產生 MCID 的必要項目之外，這個參數還能當做發行者 ID 的值 (Media Analytics 會根據該 ID 執行[同盟規則比對](/help/use-cases/federated-analytics.md))。

### Analytics 舊版使用者 ID (aid) 和宣告使用者 ID (customerID)

* **analytics.aid：**

  這個索引鍵的值必須是代表 Analytics 舊版使用者 ID 的字串
* **visitor.customerIDs：**

  這個索引鍵的值必須是採用以下格式的物件：

  ```js
  "<<insert your ID name here>>": {  
    "id": " <<insert your id here>>",  
     "authState": <<insert one of 0, 1, 2>>
  }
  ```

請注意，`visitor.customerIDs` 值可以在呈現的格式內加入任意數量的物件。

### visitor.aamLocationHint

這個參數指出當 Adobe Analytics 將客戶資料傳送到 Audience Manager 時的目的地 Adobe Audience Manager (AAM) Edge。如果未輸入值，則為空值。當使用者傾向於在偏遠位置使用裝置 (如美國東部、美國西部、歐洲、亞洲) 時，這個參數尤其重要。否則，使用者資料將散佈到多個 AAM Edge。

### media.resume

如果應用程式判斷工作階段先前曾關閉，並在稍後恢復 (例如，使用者離開視訊，但後來繼續播放)，而且播放器從停止的播放點恢復視訊播放，您可以在 **呼叫的參數儲存貯體中傳送選用的布林值** media.resume`sessionStart` 參數。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
