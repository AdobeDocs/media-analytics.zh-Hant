---
title: 啟用媒體報表
description: 了解收集媒體量度的媒體報表套裝。  遵循這些步驟，在傳送媒體資料之前設定媒體報表。
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# 啟用媒體報表

在傳送媒體資料之前，必須先設定好收集媒體量度的每個報表套裝。

1. 在[Adobe Analytics](https://experience.adobe.com/analytics)中，瀏覽至&#x200B;**[!UICONTROL 管理員]** → **[!UICONTROL 報表套裝]**。
1. 選取收集媒體資料的報表套裝。 選取&#x200B;**[!UICONTROL 編輯設定]** → **[!UICONTROL 媒體管理]** → **[!UICONTROL 媒體報告]**。

   ![報表套裝管理員功能表熒幕擷圖](assets/media-reporting.png)

1. 在&#x200B;**[!UICONTROL 媒體報表]**&#x200B;頁面上，啟用所需的串流媒體元件（請參閱下文）。

1. 選取&#x200B;**[!UICONTROL 儲存].**

   若此報表套裝已設定來收集媒體資料，在您按一下&#x200B;**[!UICONTROL 「儲存」]**&#x200B;後，將顯示另一個設定頁面。 如果您看見&#x200B;**[!UICONTROL 「媒體核心測量」]**&#x200B;頁面，請繼續進行下一個步驟。

## 可用的串流媒體模組

媒體測量包含下列模組:

* **[!UICONTROL 媒體核心]**：所有串流媒體追蹤都需要。 它會保留解決方案變數以用於內容播放和工作階段資料。
   * **維度：**
      * [[!UICONTROL 內容]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL 內容頻道]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL 內容長度（變數）]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL 內容名稱（變數）]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL 內容播放器名稱]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL 內容區段]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL 內容型別]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL 媒體路徑]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL 媒體工作階段識別碼]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL 資料流型別]](/help/reporting/dimensions/stream-type.md)
   * **量度：**
      * [[!UICONTROL 平均分鐘觀眾數]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL 內容完成]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL 內容繼續]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL 內容區段檢視]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL 內容開始]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL 內容逗留時間]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL 媒體開始]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL 暫停事件]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL 已暫停受影響的資料流]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL 進度標籤]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL 總暫停期間]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL 不重複播放時間]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL 媒體廣告]**：啟用媒體內容內廣告的追蹤功能。
   * **維度：**
      * [[!UICONTROL 廣告]](/help/reporting/dimensions/ad.md)
      * [Pod位置中的[!UICONTROL 廣告]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL 廣告長度（變數）]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL 廣告名稱（變數）]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL 廣告播放器名稱]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL 廣告Pod]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL 廣告商]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL 行銷活動 ID]](/help/reporting/dimensions/campaign-id.md)
   * **分類維度：**
      * [[!UICONTROL 資產ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL 內容評等]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL 首播日期]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL 第一個數位日期]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Pod名稱]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Pod位置]](/help/reporting/dimensions/pod-position.md)
   * **量度：**
      * [[!UICONTROL 廣告完成]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL 廣告開始]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL 廣告逗留時間]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL 媒體逗留時間]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL 媒體章節]**：啟用媒體內容中章節的追蹤功能。
   * **Dimension：**
      * [[!UICONTROL 章節]](/help/reporting/dimensions/chapter.md)
   * **分類維度：**
      * [[!UICONTROL 章節長度]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL 章節名稱]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL 章節位移]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL 章節位置]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL 創作者]](/help/reporting/dimensions/originator.md)
   * **量度：**
      * [[!UICONTROL 章節完成]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL 章節逗留時間]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL 媒體品質]**：啟用播放品質資料的追蹤功能，包括緩衝、位元速率和錯誤事件。
   * **維度：**
      * [[!UICONTROL 平均位元速率]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL 位元速率變更]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL 緩衝事件]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL 掉格]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL 個錯誤]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL 外部錯誤識別碼]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL 播放器SDK錯誤ID]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL 開始時間]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL 總緩衝期間]](/help/reporting/dimensions/total-buffer-duration.md)
   * **量度：**
      * [[!UICONTROL 平均位元速率]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL 位元速率變更影響的資料流]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL 位元速率變更]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL 緩衝事件]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL 緩衝影響的資料流]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL 掉格影響的資料流]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL 掉格]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL 開始前掉格]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL 錯誤事件]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL 錯誤影響的資料流]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL 開始時間]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL 總緩衝期間]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL 視訊中繼資料]**：啟用追蹤標準視訊內容屬性的功能，例如節目、季節和型別。
   * **維度：**
      * [!UICONTROL 個廣告載入]
      * [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL 集]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL 型別]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL 媒體摘要型別]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL 網路]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL 季]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL 節目]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL 顯示型別]](/help/reporting/dimensions/show-type.md)
   * **量度：**
      * [[!UICONTROL 已授權]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL 音訊中繼資料]**：啟用標準音訊內容屬性的追蹤功能，例如演出者、專輯和電台。
   * **維度：**
      * [[!UICONTROL 相簿]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL 藝人]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 作者]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Label]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 發行者]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 電台]](/help/reporting/dimensions/station.md)
* **[!UICONTROL 播放器狀態追蹤]**：啟用標準播放器UI狀態的測量，例如全熒幕、隱藏式字幕和子母畫面。
   * **量度：**
      * [[!UICONTROL 隱藏式字幕計數]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL 隱藏式字幕總時間]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL 全熒幕次數]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL 全熒幕總時間]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL 觀看中次數]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL 觀看中總時間]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL 靜音計數]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL 靜音總時間]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL 子母畫面計數]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL 子母畫面總時間]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL 受隱藏式字幕影響的資料流]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL 受全熒幕影響的資料流]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL 受觀看中影響的資料流]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL 受靜音影響的資料流]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL 受子母畫面影響的資料流]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)
