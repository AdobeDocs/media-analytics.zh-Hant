---
seo-title: 要求參數
title: 要求參數
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 5fc38098bcd497f3305f76ae2b23757b5f81ac69

---


# 要求參數{#request-parameters}

## Analytics 資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | Adobe Analytics 伺服器的 URL |
| `analytics.reportSuite` | Y | `sessionStart` | 識別 Analytics 報表資料的 ID |
| `analytics.enableSSL` | N | `sessionStart` | 是否啟用 SSL (True 或 False) |
| `analytics.visitorId` | N | `sessionStart` | Adobe訪客ID是可跨多個Adobe應用程式使用的自訂ID。 心率 `visitorId` 等於分析 `VID.` |

## 訪客資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Experience Cloud 組織 ID，能在 Adobe Experience Cloud 生態系統中識別您的組織 |
| `visitor.marketingCloudUserId` | N | `sessionStart` | 這是Experience cloud使用者ID(ECID)。 在大多數情況下，這是您用來識別使用者的ID。 「心率」 `marketingCloudUserId` 等於 `MID` Adobe Analytics中的。 雖然在技術上並非必要，但存取Experience cloud系列應用程式時，此參數是必要的。 |
| `visitor.aamLocationHint` | N | `sessionStart` | 提供 Adobe Audience Manager Edge 資料 |
| `appInstallationId` | N | `sessionStart` | 唯一識別應用程式和裝置的 appInstallationId |

## 內容資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | 內容的唯一識別碼 |
| `media.name` | N | `sessionStart` | 內容的人類可讀名稱 |
| `media.length` | Y | `sessionStart` | 內容長度 (秒) |
| `media.contentType` | Y | `sessionStart` | 資料流的格式 (可以是任何字串；幾個建議的值包括「即時」、「VOD」或「線性」) |
| `media.playerName` | Y | `sessionStart` | 負責轉譯內容之播放器的名稱 |
| `media.channel` | Y | `sessionStart` | 內容分送的管道。可以是行動應用程式名稱或網站名稱、屬性名稱 |
| `media.resume` | N | `sessionStart` | 指出使用者是否正在繼續先前的作業（與啟動新作業相反） |
| `media.sdkVersion` | N | `sessionStart` | 播放器使用的 SDK 版本 |

## 內容標準中繼資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | 節目或影集名稱 |
| `media.season` | N | `sessionStart` | 節目或影集隸屬的季數 |
| `media.episode` | N | `sessionStart` | 集數 |
| `media.assetId` | N | `sessionStart` | 視訊資產的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。 |
| `media.genre` | N | `sessionStart` | 內容製作人定義的內容類型 |
| `media.firstAirDate` | N | `sessionStart` | 內容在電視上的首播日期 |
| `media.firstDigitalDate` | N | `sessionStart` | 內容在任何數位平台上的首播日期 |
| `media.rating` | N | `sessionStart` | 依美國電視分級制度 (TV Parental Guidelines) 的定義進行分級 |
| `media.originator` | N | `sessionStart` | 內容的建立者 |
| `media.network` | N | `sessionStart` | 網路 / 頻道名稱 |
| `media.showType` | N | `sessionStart` | 內容的類型，以 0 到 3 的整數來表示: <ul> <li>0 – 全集 </li> <li>1 – 預覽 </li> <li>2 – 片段 </li> <li>3 – 其他 </li> </ul> |
| `media.adLoad` | N | `sessionStart` | 載入的廣告類型 |
| `media.pass.mvpd` | N | `sessionStart` | Adobe 驗證提供的 MVPD |
| `media.pass.auth` | N | `sessionStart` | 指出使用者已獲得 Adobe 驗證授權 (若有設定，只能為 True) |
| `media.dayPart` | N | `sessionStart` | 內容播出當天的時間 |
| `media.feed` | N | `sessionStart` | 摘要類型，如 "West-HD" |

## 廣告資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | 廣告插播的易記名稱 |
| `media.ad.podIndex` | Y | `adBreakStart` | 視訊中的廣告 Pod 索引 |
| `media.ad.podSecond` | Y | `adBreakStart` | Pod 開始的秒數 |
| `media.ad.podPosition` | Y | `adStart` | 廣告插播中的廣告索引，從 1 開始 |
| `media.ad.name` | N | `adStart` | 廣告的易記名稱 |
| `media.ad.id` | Y | `adStart` | 廣告名稱 |
| `media.ad.length` | Y | `adStart` | 視訊廣告長度 (以秒為單位) |
| `media.ad.playerName` | Y | `adStart` | 負責轉譯廣告之播放器的名稱 |

## 廣告標準中繼資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | 廣告中精選產品的公司或品牌 |
| `media.ad.campaignId` | N | `adStart` | 廣告促銷活動 ID |
| `media.ad.creativeId` | N | `adStart` | 廣告創意 ID |
| `media.ad.siteId` | N | `adStart` | 廣告網站 ID |
| `media.ad.creativeURL` | N | `adStart` | 廣告創意的 URL |
| `media.ad.placementId` | N | `adStart` | 廣告版位 ID |

## 章節資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | 識別章節在內容中的位置 |
| `media.chapter.offset` | Y | `chapterStart` | 章節開始播放的秒數 |
| `media.chapter.length` | Y | `chapterStart` | 章節的長度 (以秒為單位) |
| `media.chapter.friendlyName` | N | `chapterStart` | 章節的人類易記名稱 |

## 品質資料

| 請求金鑰 | 必填 | 設定於... |  說明  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | 任何 | 資料流的位元速率 |
| `media.qoe.droppedFrames` | N | 任何 | 資料流掉格的數量 |
| `media.qoe.framesPerSecond` | N | 任何 | 每秒時間格數量 |
| `media.qoe.timeToStart` | N | 任何 | 從使用者點擊播放到內容載入並開始播放之間的時間量 (以毫秒為單位) |

## 其他詳細資料 {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. 如果您已經與 Experience Cloud 產品整合，而且已取得 MCID，這項功能將會非常實用。

>[!NOTE]
>
>Media Analytics(MA)已與Experience cloud應用程式系列（Adobe Analytics、Audience Manager、Target等）整合。 若要存取這些應用程式，您需要 Experience Cloud ID。_ECID是您在大多數情況下識別使用者時應使用的ECID。_

### appInstallationId

* **如果您&#x200B;*未傳遞值*-`appInstallationId`** MA後端將不再產生MCID，但會依賴Adobe Analytics來完成此作業。 Adobe 建議您盡可能傳送 MCID 或 `appInstallationId` (連同目前仍為必要項目的 `marketingCloudOrgId`)，讓媒體收集 API 在每次呼叫時產生 MCID 並予以傳送。

* **如果&#x200B;*您傳遞*值`appInstallationId`-The MCID can be** generated by the MA back-end, if you pass values for and the(required)parements **`appInstallationId``marketingCloudOrgId` . 如果您自行傳遞 `appInstallationId`，必須將其值保留在用戶端上。該值必須供裝置上的應用程式專用，而且只要您未重新安裝應用程式，該值就必須存在。

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. 每部裝置上的每個應用程式都必須有專屬的值。也就是說，假設有兩位使用者在兩部相異裝置上使用同一款應用程式的相同版本，他們必須分別傳送不同 (唯一) 的 `appInstallationId`。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](/help/federated-analytics.md))

### Analytics 舊版使用者 ID (aid) 和宣告使用者 ID (customerID)

* **analytics.aid:**

   此索引鍵的值必須是代表Analytics舊版使用者ID的字串
* **visitor.customerIDs:**

   此鍵的值必須是以下格式的對象：

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

Note that the `visitor.customerIDs` value can have any number of objects in the presented format.

### visitor.aamLocationHint

此參數指出當Adobe Analytics將客戶資料傳送至Audience Manager時，會點擊哪個Adobe Audience Manager(AAM)Edge。 如果您未傳遞這個參數，Adobe 會將其硬式編碼為 1。當使用者傾向於在偏遠位置使用裝置 (如美國東部、美國西部、歐洲、亞洲) 時，這個參數尤其重要。否則，使用者資料將散佈到多個 AAM Edge。

### media.resume

如果應用程式判斷工作階段先前曾關閉，並在稍後恢復 (例如，使用者離開視訊，但後來繼續播放)，而且播放器從停止的播放點恢復視訊播放，您可以在 **呼叫的參數儲存貯體中傳送選用的布林值** media.resume`sessionStart` 參數。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
