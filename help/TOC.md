---
product: Media Analytics
audience: 終端使用者
user-guide-title: 音訊與視訊專用的Adobe Analytics
translation-type: tm+mt
source-git-commit: 65a9ae618a7d96f0571cff47bdc47e5b77a3745e

---


# Adobe Analytics for Audio and Video {#using}

+ [在Adobe Analytics中測量音訊和視訊](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [里程碑概述](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [將里程碑移轉至媒體分析](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [從里程碑移轉至自訂連結](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Analytics 中的自訂連結 {#cl-in-aa}
      + [自訂連結實作指南](measurement-options/cl-in-aa/cl-impl-guide.md)
+ 音訊和視訊分析簡介 {#intro-to-ava}
   + [必要條件](intro-to-ava/prereqs.md)
   + 實施路徑 {#implementation-paths}
      + [概述](intro-to-ava/implementation-paths/implementation-paths.md)
      + [用戶端](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Audience Manager 啟用](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [下載 SDK](sdk-implement/download-sdks.md)
   + 設定和配置 {#setup}
      + [概述](sdk-implement/setup/setup-overview.md)
      + [設定 Android](sdk-implement/setup/set-up-android.md)
      + [設定 iOS](sdk-implement/setup/set-up-ios.md)
      + [設定 JavaScript](sdk-implement/setup/set-up-js.md)
      + [設定 Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [設定 Roku](sdk-implement/setup/set-up-roku.md)
   + 追蹤音效和視訊播放 {#track-av-playback}
      + [概述](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [在Android上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [在iOS上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [在JavaScript上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [在Chromecast上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [在Roku上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [在Android上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [在iOS上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [追蹤JavaScript上的緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Chromecast上的追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在Roku上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [Android上的追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [在iOS上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [在JavaScript上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Chromecast的追蹤](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Roku上的追蹤](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 實作標準中繼資料 {#impl-std-metadata}
         + [在 Android 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [在 iOS 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS中繼資料索引鍵](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [在 JavaScript 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [在 Chromecast 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [標準中繼資料參數- Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [標準中繼資料參數- Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 追蹤廣告 {#track-ads}
      + [概述](sdk-implement/track-ads/track-ads-overview.md)
      + [在Android上追蹤廣告](sdk-implement/track-ads/track-ads-android.md)
      + [在iOS上追蹤廣告](sdk-implement/track-ads/track-ads-ios.md)
      + [在JavaScript上追蹤廣告](sdk-implement/track-ads/track-ads-js.md)
      + [在Chromecast上追蹤廣告](sdk-implement/track-ads/track-ads-chromecast.md)
      + [在Roku上追蹤廣告](sdk-implement/track-ads/track-ads-roku.md)
      + 實作標準廣告中繼資料 {#impl-std-ad-metadata}
         + [在 Android 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [在 iOS 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [在 JavaScript 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [在 Roku 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 追蹤章節和區段 {#track-chapters}
      + [概述](sdk-implement/track-chapters/track-chapters-overview.md)
      + [在Android上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-android.md)
      + [在iOS上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-ios.md)
      + [在JavaScript上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-js.md)
      + [追蹤Chromecast上的章節和區段](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [追蹤Roku上的章節和區段](sdk-implement/track-chapters/track-chapters-roku.md)
   + 追蹤體驗品質 {#track-qos}
      + [概述](sdk-implement/track-qos/track-qos-overview.md)
      + [在Android上追蹤體驗品質](sdk-implement/track-qos/track-qos-android.md)
      + [在iOS上追蹤體驗品質](sdk-implement/track-qos/track-qos-ios.md)
      + [在JavaScript上追蹤體驗品質](sdk-implement/track-qos/track-qos-js.md)
      + [追蹤Chromecast的體驗品質](sdk-implement/track-qos/track-qos-chromecast.md)
      + [追蹤Roku的體驗品質](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [概述](sdk-implement/track-errors/track-errors-overview.md)
      + [在Android上追蹤錯誤](sdk-implement/track-errors/track-errors-android.md)
      + [在iOS上追蹤錯誤](sdk-implement/track-errors/track-errors-ios.md)
      + [在JavaScript上追蹤錯誤](sdk-implement/track-errors/track-errors-js.md)
      + [在Chromecast上追蹤錯誤](sdk-implement/track-errors/track-errors-chromecast.md)
      + [在Roku上追蹤錯誤](sdk-implement/track-errors/track-errors-roku.md)
   + [退出與隱私權](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
      + [沒有廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [具有前段廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [具有已略過廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [具有一個章節的 VOD 播放](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [具有已略過章節的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [主要內容中具有搜尋的 VOD 播放](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [具有緩衝的 VOD 播放](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [多個 VOD 追蹤器並行](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [用於多個工作階段的 VOD 一個追蹤器](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [即時主要內容](sdk-implement/tracking-scenarios/live-main-content.md)
      + [具有循序追蹤的即時主要內容](sdk-implement/tracking-scenarios/live-sequential.md)
   + 驗證 {#validation}
      + [驗證概觀](sdk-implement/validation/validation-overview.md)
      + [測試 1: 標準播放](sdk-implement/validation/test1-standard-playback.md)
      + [測試2:媒體中斷](sdk-implement/validation/test2-media-interrupt.md)
      + [測試呼叫詳細資訊](sdk-implement/validation/test-call-details.md)
      + [心率參數說明](sdk-implement/validation/heartbeat-params.md)
      + 除錯 {#debugging}
         + [SDK除錯](sdk-implement/validation/debugging/sdk-debugging.md)
         + [設定 Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [建立新的 Debug 報表](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Debug 控制面板和報表](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [追蹤應用程式狀態](sdk-implement/analytics-with-ott/track-app-states.md)
      + [追蹤應用程式動作](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [設定使用者ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT 與 Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT 與 Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + 逐步指南 {#cookbook}
      + [在播放期間處理應用程式中斷](sdk-implement/cookbook/app-interrupts.md)
      + [解決 main:play 出現在廣告之間的問題](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [繼續非活動會話](sdk-implement/cookbook/resuming-inactive.md)
      + [在 SceneGraph (Roku) 中進行追蹤](sdk-implement/cookbook/sdk-track-scenegraph.md)
      + [SDK與啟動差異](sdk-implement/cookbook/sdk-vs-launch-qoe.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [移轉概述](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [程式碼比較: 1.x 和 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [從 1.x 轉換為 2.x API](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ Media Collection API(RESTful) {#media-collection-api}
   + [概述](media-collection-api/mc-api-overview.md)
   + API 參考 {#mc-api-ref}
      + [工作階段要求](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [事件要求](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [要求參數](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [事件類型和說明](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON 驗證結構](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + 實作 API {#mc-api-impl}
      + [快速啟動](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [在播放器中設定 HTTP 要求類型](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [取得工作階段 ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [實作事件要求](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [驗證事件要求](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [傳送 Ping 事件](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [傳送 QoE 資料](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [自訂中繼資料支援](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [逾時條件](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [控制事件順序](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [在工作階段回應緩慢時將事件加入佇列](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Media Tracking Timelines {#mc-api-timelines}
      + [時間軸 1 - 檢視內容到結束為止](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [時間軸 2 - 使用者放棄工作階段](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [時間軸 3 - 章節](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [追蹤下載的內容](media-collection-api/track-downloaded-content.md)
+ 量度和中繼資料 {#metrics-and-metadata}
   + [音訊和視訊參數](metrics-and-metadata/audio-video-parameters.md)
   + [廣告參數](metrics-and-metadata/ad-parameters.md)
   + [章節參數](metrics-and-metadata/chapter-parameters.md)
   + [品質參數](metrics-and-metadata/quality-parameters.md)
   + [區段](metrics-and-metadata/segments.md)
   + [計算量度](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [媒體報告啟用](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [預設報表概述](media-reports/media-default-reports/default-reports-overview.md)
      + [媒體概述](media-reports/media-default-reports/media-reports-overview.md)
      + [媒體詳細資料](media-reports/media-default-reports/media-reports-detail.md)
      + [媒體播出時段](media-reports/media-default-reports/media-reports-daypart.md)
      + [媒體同時觀看者](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [取得同時觀看者 JSON 報表資料](media-reports/media-default-reports/get-concurrent-json.md)
   + [媒體工作區範本](media-reports/media-workspace-templates.md)
+ [同盟分析](data-sharing/federated-analytics.md)
+ 其他資源 {#additional-resources}
   + [文件更新](additional-resources/doc-updates.md)
