---
title: 將受眾移轉至適用於串流媒體的新的Adobe Analytics資料型別
description: 瞭解如何將受眾移轉至適用於串流媒體的新的Adobe Analytics資料型別
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 44%

---

# 適用於Adobe Experience Platform和Customer Journey Analytics的Media Analytics引數對應

本檔案提供Adobe Experience Platform和Customer Journey Analytics中所有Media Analytics使用引數的完整清單。 其目的是支援將透過[Analytics Source Connector](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)或[Analytics Source Connector for Classifications](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/classifications)從Adobe Analytics匯入的資料整合到Platform，並將每個引數對應到其對應的XDM欄位路徑。

## Media Analytics保留變數

對於所有Media Analytics保留變數，下表所指出的「目前XDM欄位路徑」下方，提供從Adobe Analytics擷取到2025年5月（及包括）的AEP資料。

由於Media Analytics和ADC團隊目前正致力於完全移轉至「報告XDM欄位路徑」，在此移轉完成且「報告XDM欄位路徑」可供使用後，將會共用正式通訊。

## 串流媒體引數

| 欄位名稱 | 目前的XDM欄位路徑（已棄用） | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 備註 |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| 串流類型 | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | 維度 | 串流類型 |                                                                       |
| 內容 ID | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | 維度 | 內容 ID |                                                                       |
| 內容長度 | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | 維度 | 內容長度 |                                                                       |
| 內容類型 | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | 維度 | 內容類型 |                                                                       |
| 媒體工作階段 ID | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | 維度 | 媒體工作階段 ID |                                                                       |
| 內容播放器名稱 | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | 維度 | 內容播放器名稱 |                                                                       |
| 內容頻道 | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | 維度 | 內容頻道 |                                                                       |
| 內容區段 | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | 維度 | 內容區段 |                                                                       |
| 內容名稱 | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | 維度 | 內容名稱 |                                                                       |
| 影片路徑 | *未用於AEP/CJA* |                                                   |           |                   | Adobe Analytics特定屬性 |
| 節目 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | 維度 | 節目 |                                                                       |
| 季數 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | 維度 | 季數 |                                                                       |
| 集數 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | 維度 | 集數 |                                                                       |
| 類型 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | 維度 | 不支援 | 使用「媒體報表」欄位 |
| 網路 | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | 維度 | 網路 |                                                                       |
| 節目類型 | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | 維度 | 節目類型 |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | 維度 | MVPD |                                                                       |
| 已驗證 | 不支援 | mediaReporting.sessionDetails.authorized | 維度 | 已驗證 |                                                                       |
| 時段 | 不支援 | mediaReporting.sessionDetails.dayPart | 維度 | 時段 |                                                                       |
| 媒體摘要類型 | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | 維度 | 媒體摘要類型 |                                                                       |
| 藝術家 | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | 維度 | 藝人 |                                                                       |
| 專輯 | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | 維度 | 專輯 |                                                                       |
| 標籤 | 不支援 | mediaReporting.sessionDetails.label | 維度 | 標籤 |                                                                       |
| 作者 | 不支援 | mediaReporting.sessionDetails.author | 維度 | 作者 |                                                                       |
| 電台 | media.mediaTimed.primaryAssetReference._id3.音訊。_id3.TRSN | mediaReporting.sessionDetails.station | 維度 | 電台 |                                                                       |
| 發行者 | media.mediaTimed.primaryAssetReference._id3.音訊。_id3.TPUB | mediaReporting.sessionDetails.publisher | 維度 | 發行者 |                                                                       |
| 媒體開始次數 | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | 量度 | 媒體開始次數 |                                                                       |
| 內容開始 | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | 量度 | 內容開始 |                                                                       |
| 內容完成 | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | 量度 | 內容完成 |                                                                       |
| 內容逗留時間 | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | 量度 | 內容逗留時間 |                                                                       |
| 媒體逗留時間 | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | 量度 | 媒體逗留時間 |                                                                       |
| 不重複播放時間 | 不支援 | mediaReporting.sessionDetails.uniqueTimePlayed | 量度 | 不重複播放時間 |                                                                       |
| 10% 進度標記 | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | 量度 | 10% 進度標記 |                                                                       |
| 25% 進度標記 | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | 量度 | 25% 進度標記 |                                                                       |
| 50% 進度標記 | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | 量度 | 50% 進度標記 |                                                                       |
| 75% 進度標記 | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | 量度 | 75% 進度標記 |                                                                       |
| 95% 進度標記 | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | 量度 | 95% 進度標記 |                                                                       |
| 平均分鐘觀眾數 | 不支援 | mediaReporting.sessionDetails.averageMinuteAudience | 量度 | 平均分鐘觀眾數 |                                                                  |
| 上次通話後經過秒數 | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | 量度 | 上次通話後經過秒數 |                                                              |
| 暫停的受影響資料流 | 不支援 | mediaReporting.sessionDetails.hasPauseImpactedStreams | 量度 | 暫停的受影響資料流 | 我們會透過從其他事件計算此值來涵蓋mediaTimed |
| 暫停事件 | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | 量度 | 暫停事件 |                                                                       |
| 總暫停期間 | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | 量度 | 總暫停期間 |                                                                       |
| 內容恢復 | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | 量度 | 內容恢復 |                                                                       |
| 內容區段檢視次數 | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | 量度 | 內容區段檢視次數 |                                                                     |

{style="table-layout:auto"}

## 播放器狀態引數更新

| 欄位名稱 | 目前的XDM欄位路徑（已棄用） | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 備註 |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| 受播放器狀態影響的資料流 | 不支援 | mediaReporting.states.isSet | 量度 | 不支援 | 使用mediaReporting欄位 |
| 播放器狀態計數 | 不支援 | mediaReporting.states.count | 量度 | 不支援 | 使用mediaReporting欄位 |
| 播放器狀態總時間 | 不支援 | mediaReporting.states.time | 量度 | 不支援 | 使用mediaReporting欄位 |
| 播放器狀態名稱 | 不支援 | mediaReporting.states.name | 維度 | 不支援 | 使用mediaReporting欄位 |

{style="table-layout:auto"}

## 章節參數

| 欄位名稱 | 目前的XDM欄位路徑（已棄用） | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 備註 |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| 章節 | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | 維度 | 章節 |           |
| 章節開始 | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | 量度 | 章節開始 |           |
| 章節完成 | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | 量度 | 章節完成 |          |
| 章節逗留時間 | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | 量度 | 章節逗留時間 |        |

{style="table-layout:auto"}

## 廣告參數

| 欄位名稱 | 目前的XDM欄位路徑（已棄用） | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 備註 |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 廣告 ID | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | 維度 | 廣告 ID |           |
| Pod 位置中的廣告 | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | 維度 | Pod 位置中的廣告 |     |
| 廣告長度 | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | 量度 | 廣告長度 |           |
| 廣告播放器名稱 | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | 維度 | 廣告播放器名稱 |           |
| 廣告插播 ID | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | 維度 | 廣告插播 ID |           |
| 廣告名稱 | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | 維度 | 廣告名稱 |           |
| 廣告商 | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | 維度 | 廣告商 |           |
| 行銷活動 ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | 維度 | 行銷活動 ID |           |
| 廣告開始 | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | 量度 | 廣告開始 |           |
| 廣告完成 | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | 量度 | 廣告完成 |           |
| 廣告逗留時間 | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | 量度 | 廣告逗留時間 |           |

{style="table-layout:auto"}

## 品質參數

| 欄位名稱 | 目前的XDM欄位路徑（已棄用） | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 備註 |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 平均位元速率 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage |   | 平均位元速率 |           |
| 開始時間 | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart |   | 開始時間 |           |
| 掉格 | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames |   | 掉格 |           |
| 緩衝事件 | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount |   | 緩衝事件 |           |
| 總緩衝期間 | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime |   | 總緩衝期間 |     |
| 位元速率變更 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount |   | 位元速率變更 |         |
| 錯誤/錯誤事件 | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount |   | 錯誤/錯誤事件 |  |
| 播放器 SDK 錯誤 ID | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | 維度 | 不支援 | 使用mediaReporting欄位 |
| 外部錯誤 ID | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | 維度 | 不支援 | 使用mediaReporting欄位 |
| 開始前掉格 | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | 量度 | 開始前掉格 |     |
| 緩衝影響的資料流 | 不支援 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | 量度 | 緩衝影響的資料流 | 從其他事件計算 |
| 位元速率變更影響的資料流 | 不支援 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | 量度 | 位元速率變更影響的資料流 | 從其他事件計算 |
| 錯誤影響的資料流 | 不支援 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | 量度 | 錯誤影響的資料流 | 從其他事件計算 |
| 掉格影響的資料流 | 不支援 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | 量度 | 掉格影響的資料流 | 從其他事件計算 |

{style="table-layout:auto"}

## Media Analytics分類

Media Analytics分類會透過稱為ACDC的個別流程內嵌至AEP中。 下表列出的每個分類群組都與AEP中的唯一資料集相對應。 在CJA中，必須在Media Analytics事件資料集和每個分類資料集之間建立連線。

### 在Customer Journey Analytics中連線資料集

若要在Customer Journey Analytics中設定連線：

- 瀏覽至&#x200B;**連線**&#x200B;標籤，並選取&#x200B;**建立新連線**。
- 在「連線」介面中，選擇&#x200B;**新增資料集**，並找到Media Analytics事件資料集（用於透過ADC匯入媒體資料）以及四個相關的分類資料集。

### 設定詳細資料

針對每個查詢資料集（分類資料集），設定如下：

- **視訊資料集**：
   - 索引鍵： `_sandbox.key`
   - 比對索引鍵： `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - 資料來源型別： `Web Data`

- **視訊資料集**：
   - 索引鍵： `_sandbox.key`
   - 比對索引鍵： `Ad ID (advertising.adAssetReference._id)`
   - 資料來源型別： `Web Data`

- **videoadpod資料集**：
   - 索引鍵： `_sandbox.key`
   - 比對索引鍵： `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - 資料來源型別： `Web Data`

- **videochapter資料集**：
   - 索引鍵： `_sandbox.key`
   - 比對索引鍵： `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - 資料來源型別： `Web Data`

### 報表考量事項

在報告期間使用分類資料集時，請確定您參考分類特定欄位路徑(`ACDC XDM Path`)，而不是標準Media Analytics XDM欄位。

## 分類表格

| 分類名稱（群組） | 欄位名稱 | ACDC XDM路徑 |
|------------|----------|-------------|
| video | 金鑰/資產ID | `<_sandbox>.key` |
| video | 影片長度 | `<_sandbox>.video_length` |
| video | 影片名稱 | `<_sandbox>.video_name` |
| video | 資產 ID | `<_sandbox>.asset_id` |
| video | 首播日期 | `<_sandbox>.first_air_date` |
| video | 首次數位化日期 | `<_sandbox>.first_digital_date` |
| video | 內容評等 | `<_sandbox>.content_rating` |
| video | 創作者 | `<_sandbox>.originator` |
| videoad | 金鑰/廣告ID | `<_sandbox>.key` |
| videoad | 廣告長度 | `<_sandbox>.ad_length` |
| videoad | 廣告名稱 | `<_sandbox>.ad_name` |
| videoad | 創作 ID | `<_sandbox>.creative_id` |
| videoadpod | 索引鍵/廣告Pod ID | `<_sandbox>.key` |
| videoadpod | Pod 位置 | `<_sandbox>.pod_position` |
| videoadpod | Pod 名稱 | `<_sandbox>.pod_name` |
| videochapter | 索引鍵/章節 | `<_sandbox>.key` |
| videochapter | 章節長度 | `<_sandbox>.chapter_length` |
| videochapter | 章節位移 | `<_sandbox>.chapter_offset` |
| videochapter | 章節位置 | `<_sandbox>.chapter_position` |
| videochapter | 章節名稱 | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Media Analytics自訂變數

在Adobe Analytics中，自訂變數會根據每個報表套裝中所定義的實作規則，指派給不同的事件或eVar。 因此，當這些自訂變數匯入Adobe Experience Platform (AEP)時，它們會對映至不同的XDM路徑。

- 事件儲存在路徑下：

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVar儲存在路徑下：

  `_experience.analytics.customDimensions.eVars.eVar<number>`

在這兩種情況下，`<number>`都會對應至原始Adobe Analytics報表套裝設定中使用的特定事件或eVar編號。

### 自訂變數

| 欄位名稱 | XDM路徑 | 資料類型 |
|-------------|-------------|-----------|
| 下載的媒體標幟 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| SDK 版本 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| VHL 版本 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 資料流格式 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 首播日期 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 首次數位化日期 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 同盟資料 | `_experience.analytics.customDimensions.eVars.eVar<number>` 與 `_experience.analytics.event<x>to<y>.event<number>.value` |   |
| 預估資料流量 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 廣告計數 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 章節計數 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 創作 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 網站 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 創作 URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 版面 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 維度 |
| 每秒影格數 | `_experience.analytics.customDimensions.eVars.eVar<number>` 與 `_experience.analytics.event<x>to<y>.event<number>.value` |   |
| Media SDK 錯誤 ID | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 停頓影響的資料流 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 停頓事件 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 總停頓期間 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |

{style="table-layout:auto"}
