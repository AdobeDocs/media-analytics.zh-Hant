---
title: 適用於Adobe Experience Platform和Customer Journey Analytics的Media Analytics引數對應
description: 搭配Analytics Source Connector和Customer Journey Analytics使用的Media Analytics引數的XDM欄位路徑對應。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 1325
ht-degree: 20%

---

# 適用於Adobe Experience Platform和Customer Journey Analytics的Media Analytics引數對應

本檔案提供Adobe Experience Platform和Customer Journey Analytics中所有Media Analytics使用引數的完整清單。 其目的是支援將透過[Analytics Source Connector](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)或[Analytics Source Connector for Classifications](https://experienceleague.adobe.com/tw/en/docs/experience-platform/sources/connectors/adobe-applications/classifications)從Adobe Analytics匯入的資料整合到Platform，並將每個引數對應到其對應的XDM欄位路徑。

>[!NOTE]
>
>此參考資料適用於使用[Analytics來源聯結器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)將串流媒體資料從Adobe Analytics帶入Adobe Experience Platform，以搭配Customer Journey Analytics報表或其他Platform服務使用的組織。 這些變更不會影響作為獨立應用程式的Adobe Analytics，包括資料收集、處理和報告。

## Media Analytics保留變數

自2025年10月起，`media.mediaTimed` XDM欄位路徑已完全棄用，並由`mediaReporting`取代。 2025年10月之後擷取的資料僅包含`mediaReporting`欄位。 舊版欄位路徑下仍可使用舊版資料，反映在&#x200B;**舊版XDM欄位**&#x200B;下方的表格中。

### 保持連線呼叫行為

有了適用於串流媒體的Analytics來源聯結器，來自Adobe Analytics的持續呼叫現在會擷取到Adobe Experience Platform。 這可能會影響Customer Journey Analytics報告：

* **工作階段計數**：即使沒有直接的媒體互動，持續連線電話也能協助維持作用中的使用者工作階段。 每個媒體播放的這些呼叫會在最後一個事件後的20分鐘產生一次。 若要確保最佳工作階段追蹤，請在資料檢視中將造訪到期時間設定為30分鐘。

* **事件計數**：保持連線呼叫現在計入Customer Journey Analytics事件量度。 若要排除這些事件，請建立排除事件型別為`media.keepalive`之事件的篩選器。

## 串流媒體引數

| 欄位名稱 | 舊版XDM欄位 | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 附註 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 資料流型別]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | 維度 | [[!UICONTROL 資料流型別]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL 內容識別碼]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | 維度 | [[!UICONTROL 內容識別碼]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL 內容長度]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | 維度 | [[!UICONTROL 內容長度]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL 內容型別]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | 維度 | [[!UICONTROL 內容型別]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL 媒體工作階段識別碼]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | 維度 | [[!UICONTROL 媒體工作階段識別碼]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL 內容播放器名稱]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | 維度 | [[!UICONTROL 內容播放器名稱]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL 內容頻道]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | 維度 | [[!UICONTROL 內容頻道]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL 內容區段]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | 維度 | [[!UICONTROL 內容區段]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL 內容名稱]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | 維度 | [[!UICONTROL 內容名稱]](/help/reporting/dimensions/content-name.md) | |
| 影片路徑 | *未用於AEP/CJA* | | | | Adobe Analytics特定屬性 |
| [[!UICONTROL 節目]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | 維度 | [[!UICONTROL 節目]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL 季]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | 維度 | [[!UICONTROL 季]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL 集]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | 維度 | [[!UICONTROL 集]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL 型別]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | 維度 | 不支援 | 使用`mediaReporting`欄位 |
| [[!UICONTROL 網路]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | 維度 | [[!UICONTROL 網路]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL 顯示型別]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | 維度 | [[!UICONTROL 顯示型別]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | 維度 | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL 已授權]](/help/reporting/metrics/authorized.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | 維度 | [[!UICONTROL 已授權]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | 維度 | [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL 媒體摘要型別]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | 維度 | [[!UICONTROL 媒體摘要型別]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL 藝人]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | 維度 | [[!UICONTROL 藝人]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL 相簿]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | 維度 | [[!UICONTROL 相簿]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.label` | 維度 | [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL 作者]](/help/reporting/dimensions/author.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.author` | 維度 | [[!UICONTROL 作者]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL 電台]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | 維度 | [[!UICONTROL 電台]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL 發行者]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | 維度 | [[!UICONTROL 發行者]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | 量度 | [[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL 內容開始]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | 量度 | [[!UICONTROL 內容開始]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | 量度 | [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | 量度 | [[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL 媒體逗留時間]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | 量度 | [[!UICONTROL 媒體逗留時間]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL 不重複播放時間]](/help/reporting/metrics/unique-time-played.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | 量度 | [[!UICONTROL 不重複播放時間]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10%進度標籤]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | 量度 | [[!UICONTROL 10%進度標籤]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25%進度標籤]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | 量度 | [[!UICONTROL 25%進度標籤]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50%進度標籤]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | 量度 | [[!UICONTROL 50%進度標籤]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75%進度標籤]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | 量度 | [[!UICONTROL 75%進度標籤]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95%進度標籤]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | 量度 | [[!UICONTROL 95%進度標籤]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 平均分鐘觀眾數]](/help/reporting/metrics/average-minute-audience.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | 量度 | [[!UICONTROL 平均分鐘觀眾數]](/help/reporting/metrics/average-minute-audience.md) | |
| 上次通話後經過秒數 | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | 量度 | 上次通話後經過秒數 | |
| [[!UICONTROL 暫停的受影響資料流]](/help/reporting/metrics/paused-impacted-streams.md) | 不支援 | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | 量度 | [[!UICONTROL 暫停的受影響資料流]](/help/reporting/metrics/paused-impacted-streams.md) | 我們會透過從其他事件計算此值來涵蓋mediaTimed |
| [[!UICONTROL 暫停事件]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | 量度 | [[!UICONTROL 暫停事件]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL 總暫停期間]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | 量度 | [[!UICONTROL 總暫停期間]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL 內容繼續]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | 量度 | [[!UICONTROL 內容繼續]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL 內容區段檢視次數]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | 量度 | [[!UICONTROL 內容區段檢視次數]](/help/reporting/metrics/content-segment-views.md) | |

## 播放器狀態引數更新

| 欄位名稱 | 舊版XDM欄位 | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 附註 |
| --- | --- | --- | --- | --- | --- |
| 受播放器狀態影響的資料流 | 不支援 | `xdm.mediaReporting.`<br>`states.isSet` | 量度 | 不支援 | 使用`mediaReporting`欄位 |
| 播放器狀態計數 | 不支援 | `xdm.mediaReporting.`<br>`states.count` | 量度 | 不支援 | 使用`mediaReporting`欄位 |
| 播放器狀態總時間 | 不支援 | `xdm.mediaReporting.`<br>`states.time` | 量度 | 不支援 | 使用`mediaReporting`欄位 |
| 播放器狀態名稱 | 不支援 | `xdm.mediaReporting.`<br>`states.name` | 維度 | 不支援 | 使用`mediaReporting`欄位 |

## 章節參數

| 欄位名稱 | 舊版XDM欄位 | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 附註 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 章節]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | 維度 | [[!UICONTROL 章節]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | 量度 | [[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL 章節完成]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | 量度 | [[!UICONTROL 章節完成]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL 章節逗留時間]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | 量度 | [[!UICONTROL 章節逗留時間]](/help/reporting/metrics/chapter-time-spent.md) | |

## 廣告參數

| 欄位名稱 | 舊版XDM欄位 | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 附註 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 廣告ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | 維度 | [[!UICONTROL 廣告ID]](/help/reporting/dimensions/ad.md) | |
| Pod位置中的[[!UICONTROL 廣告]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | 維度 | Pod位置中的[[!UICONTROL 廣告]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL 廣告長度]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | 量度 | [[!UICONTROL 廣告長度]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL 廣告播放器名稱]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | 維度 | [[!UICONTROL 廣告播放器名稱]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL 廣告插播ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | 維度 | [[!UICONTROL 廣告插播ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL 廣告名稱]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | 維度 | [[!UICONTROL 廣告名稱]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL 廣告商]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | 維度 | [[!UICONTROL 廣告商]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL 行銷活動 ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | 維度 | [[!UICONTROL 行銷活動 ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL 廣告開始]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | 量度 | [[!UICONTROL 廣告開始]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL 廣告完成]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | 量度 | [[!UICONTROL 廣告完成]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL 廣告逗留時間]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | 量度 | [[!UICONTROL 廣告逗留時間]](/help/reporting/metrics/ad-time-spent.md) | |

## 品質參數

| 欄位名稱 | 舊版XDM欄位 | 報告XDM欄位路徑 | 資料類型 | 衍生欄位 | 附註 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 平均位元速率]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | 兩者 | [[!UICONTROL 平均位元速率]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL 開始時間]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | 兩者 | [[!UICONTROL 開始時間]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL 掉格]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | 兩者 | [[!UICONTROL 掉格]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL 緩衝事件]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | 兩者 | [[!UICONTROL 緩衝事件]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL 總緩衝期間]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | 兩者 | [[!UICONTROL 總緩衝期間]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL 位元速率變更]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | 兩者 | [[!UICONTROL 位元速率變更]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL 錯誤/錯誤事件]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | 兩者 | [[!UICONTROL 錯誤/錯誤事件]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL 播放器SDK錯誤ID]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | 維度 | 不支援 | 使用`mediaReporting`欄位 |
| [[!UICONTROL 外部錯誤ID]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | 維度 | 不支援 | 使用`mediaReporting`欄位 |
| [[!UICONTROL 開始前掉格]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | 量度 | [[!UICONTROL 開始前掉格]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL 緩衝影響的資料流]](/help/reporting/metrics/buffer-impacted-streams.md) | 不支援 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | 量度 | [[!UICONTROL 緩衝影響的資料流]](/help/reporting/metrics/buffer-impacted-streams.md) | 從其他事件計算 |
| [[!UICONTROL 位元速率變更影響的資料流]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 不支援 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | 量度 | [[!UICONTROL 位元速率變更影響的資料流]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 從其他事件計算 |
| [[!UICONTROL 錯誤影響的資料流]](/help/reporting/metrics/error-impacted-streams.md) | 不支援 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | 量度 | [[!UICONTROL 錯誤影響的資料流]](/help/reporting/metrics/error-impacted-streams.md) | 從其他事件計算 |
| [[!UICONTROL 掉格影響的資料流]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 不支援 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | 量度 | [[!UICONTROL 掉格影響的資料流]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 從其他事件計算 |

## Media Analytics分類

Media Analytics分類會透過稱為ACDC的個別流程內嵌至AEP中。 下表列出的每個分類群組都與AEP中的唯一資料集相對應。 在CJA中，必須在Media Analytics事件資料集和每個分類資料集之間建立連線。

### 在Customer Journey Analytics中連線資料集

若要在Customer Journey Analytics中設定連線：

* 瀏覽至&#x200B;**連線**&#x200B;標籤，並選取&#x200B;**建立新連線**。
* 在「連線」介面中，選擇&#x200B;**新增資料集**，並找到Media Analytics事件資料集（用於透過ADC匯入媒體資料）以及四個相關的分類資料集。

### 設定詳細資料

針對每個查詢資料集（分類資料集），設定如下：

* **視訊資料集**：
   * 索引鍵： `_sandbox.key`
   * 比對索引鍵： `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * 資料來源型別： `Web Data`

* **視訊資料集**：
   * 索引鍵： `_sandbox.key`
   * 比對索引鍵： `Ad ID (advertising.adAssetReference._id)`
   * 資料來源型別： `Web Data`

* **videoadpod資料集**：
   * 索引鍵： `_sandbox.key`
   * 比對索引鍵： `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * 資料來源型別： `Web Data`

* **videochapter資料集**：
   * 索引鍵： `_sandbox.key`
   * 比對索引鍵： `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * 資料來源型別： `Web Data`

### 報表考量事項

在報告期間使用分類資料集時，請確定您參考分類特定欄位路徑(`ACDC XDM Path`)，而不是標準Media Analytics XDM欄位。

## 分類表格

| 分類名稱（群組） | 欄位名稱 | ACDC XDM路徑 |
| --- | --- | --- |
| video | 金鑰/資產ID | `xdm.<_sandbox>.key` |
| video | 影片長度 | `xdm.<_sandbox>.video_length` |
| video | 影片名稱 | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL 資產ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL 首播日期]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL 首次數位化日期]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL 內容評等]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL 創作者]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | 金鑰/廣告ID | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL 廣告長度]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL 廣告名稱]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | 索引鍵/廣告Pod ID | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Pod位置]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Pod名稱]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | 索引鍵/章節 | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL 章節長度]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL 章節位移]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL 章節位置]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL 章節名稱]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Media Analytics自訂變數

在Adobe Analytics中，自訂變數會根據每個報表套裝中所定義的實作規則，指派給不同的事件或eVar。 因此，當這些自訂變數匯入Adobe Experience Platform (AEP)時，它們會對映至不同的XDM路徑。

* 事件儲存在路徑下：

  `_experience.analytics.event<x>to<y>.event<number>.value`

* eVar儲存在路徑下：

  `_experience.analytics.customDimensions.eVars.eVar<number>`

在這兩種情況下，`<number>`都會對應至原始Adobe Analytics報表套裝設定中使用的特定事件或eVar編號。

### 自訂變數

| 欄位名稱 | XDM路徑 | 資料類型 |
| --- | --- | --- |
| [[!UICONTROL 媒體已下載旗標]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| SDK 版本 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| 媒體庫版本 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 資料流格式]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 首播日期]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 首次數位化日期]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 同盟資料]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>和<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 兩者 |
| [[!UICONTROL 預估資料流]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 個廣告計數]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 章節計數]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 網站識別碼]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL Creative URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| [[!UICONTROL 位置ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 維度 |
| 每秒影格數 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>和<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 兩者 |
| Media SDK 錯誤 ID | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 延遲受影響的資料流]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 延遲事件]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| 總停頓期間[&#128279;](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
