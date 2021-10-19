---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics for Streaming Media
breadcrumb-title: Media Analytics 指南
user-guide-description: 實作 Adobe Analytics for Streaming Media。包含 Media SDK 和 Media Collection API。
sub-product: media analytics
source-git-commit: 407f17a5b1134362c6be7c6bfae909e9e66077be
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 100%

---


# Adobe Analytics for Streaming Media {#using}

+ [在 Adobe Analytics 中測量串流媒體](media-overview.md)
+ [支援的裝置和平台](measurement-options/supported-devices.md)
+ Streaming Media Analytics 簡介 {#intro-to-ava}
   + [先決條件](intro-to-ava/prereqs.md)
   + 實作路徑 {#implementation-paths}
      + [總覽](intro-to-ava/implementation-paths/implementation-paths.md)
      + [用戶端](intro-to-ava/implementation-paths/client-side-path.md)
      + 其他實作方式 {#other-paths}
         + 媒體模組里程碑追蹤 {#mm-milestone-tracking}
            + [里程碑總覽](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [從里程碑移轉至 Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [從里程碑移轉至自訂連結](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Analytics 中的自訂連結 {#cl-in-aa}
            + [自訂連結實作指南](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [啟用 Audience Manager](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Media Analytics SDK 終止支援常見問答](sdk-implement/end-of-support-faqs.md)
   + [下載 SDK](sdk-implement/download-sdks.md)
   + 設定和設置 {#setup}
      + [總覽](sdk-implement/setup/setup-overview.md)
      + [設定 Android](sdk-implement/setup/set-up-android.md)
      + [設定 iOS](sdk-implement/setup/set-up-ios.md)
      + 設定 JavaScript {#setup-javascript}
         + [設定 JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [設定 JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [設定 Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [設定 Roku](sdk-implement/setup/set-up-roku.md)
   + 追蹤串流媒體播放 {#track-av-playback}
      + [總覽](sdk-implement/track-av-playback/track-core-overview.md)
      + 追蹤核心串流媒體播放 {#track-core}
         + [在 Android 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [在 iOS 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + 在 JavaScript 上追蹤核心播放 {#track-core-javascript}
            + [在 JavaScript 2.x 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [在 JavaScript 3.x 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [在 Chromecast 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [在 Roku 上追蹤核心播放](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + 追蹤緩衝 {#track-buffering}
         + [在 Android 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [在 iOS 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + 在 JavaScript 上追蹤緩衝 {#track-buffering-js}
            + [在 JavaScript 2.x 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [在 JavaScript 3.x 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [在 Chromecast 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在 Roku 上追蹤緩衝](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + 追蹤搜尋 {#track-seeking}
         + [在 Android 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [在 iOS 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + 在 JavaScript 上追蹤搜尋 {#track-seeking-js}
            + [在 JavaScript 2.x 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [在 JavaScript 3.x 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [在 Chromecast 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [在 Roku 上追蹤搜尋](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 實作標準中繼資料 {#impl-std-metadata}
         + [在 Android 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [在 iOS 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS 中繼資料索引鍵](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + 在 JavaScript 上實作標準中繼資料 {#impl-std-md-js}
            + [在 JavaScript 2.x 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [在 JavaScript 3.x 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [在 Chromecast 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [標準中繼資料參數 - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 上實作標準中繼資料](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [標準中繼資料參數 - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 追蹤廣告 {#track-ads}
      + [總覽](sdk-implement/track-ads/track-ads-overview.md)
      + [在 Android 上追蹤廣告](sdk-implement/track-ads/track-ads-android.md)
      + [在 iOS 上追蹤廣告](sdk-implement/track-ads/track-ads-ios.md)
      + 在 JavaScript 上追蹤廣告 {#track-ads-js}
         + [在 JavaScript 2.x 上追蹤廣告](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [在 JavaScript 3.x 上追蹤廣告](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [在 Chromecast 上追蹤廣告](sdk-implement/track-ads/track-ads-chromecast.md)
      + [在 Roku 上追蹤廣告](sdk-implement/track-ads/track-ads-roku.md)
      + 實作標準廣告中繼資料 {#impl-std-ad-metadata}
         + [在 Android 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [在 iOS 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + 在 JavaScript 上實作標準廣告中繼資料 {#impl-std-ad-md-js}
            + [在 JavaScript 2.x 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [在 JavaScript 3.x 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [在 Roku 上實作標準廣告中繼資料](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 追蹤章節和區段 {#track-chapters}
      + [總覽](sdk-implement/track-chapters/track-chapters-overview.md)
      + [在 Android 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-android.md)
      + [在 iOS 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-ios.md)
      + 在 JavaScript 上追蹤章節和區段 {#track-chapters-js}
         + [在 JavaScript 2.x 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [在 JavaScript 3.x 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [在 Chromecast 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [在 Roku 上追蹤章節和區段](sdk-implement/track-chapters/track-chapters-roku.md)
   + 追蹤體驗品質 {#track-qos}
      + [總覽](sdk-implement/track-qos/track-qos-overview.md)
      + [在 Android 上追蹤體驗品質](sdk-implement/track-qos/track-qos-android.md)
      + [在 iOS 上追蹤體驗品質](sdk-implement/track-qos/track-qos-ios.md)
      + 在 JavaScript 上追蹤體驗品質 {#track-qos-js}
         + [在 JavaScript 2.x 上追蹤體驗品質](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [在 JavaScript 3.x 上追蹤體驗品質](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [在 Chromecast 上追蹤體驗品質](sdk-implement/track-qos/track-qos-chromecast.md)
      + [在 Roku 上追蹤體驗品質](sdk-implement/track-qos/track-qos-roku.md)
   + 追蹤錯誤 {#track-errors}
      + [總覽](sdk-implement/track-errors/track-errors-overview.md)
      + [在 Android 上追蹤錯誤](sdk-implement/track-errors/track-errors-android.md)
      + [在 iOS 上追蹤錯誤](sdk-implement/track-errors/track-errors-ios.md)
      + 在 JavaScript 上追蹤錯誤 {#track-errors-js}
         + [在 JavaScript 2.x 上追蹤錯誤](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [在 JavaScript 3.x 上追蹤錯誤](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [在 Chromecast 上追蹤錯誤](sdk-implement/track-errors/track-errors-chromecast.md)
      + [在 Roku 上追蹤錯誤](sdk-implement/track-errors/track-errors-roku.md)
   + [選擇退出與隱私權](sdk-implement/opt-out-privacy.md)
   + 追蹤情境 {#tracking-scenarios}
      + [沒有廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [有前段廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [已略過廣告的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [有一個章節的 VOD 播放](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [已略過章節的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [主要內容中具有搜尋功能的 VOD 播放](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [有緩衝的 VOD 播放](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [多個 VOD 追蹤器並行](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [用於多個工作階段的一個 VOD 追蹤器](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [即時主要內容](sdk-implement/tracking-scenarios/live-main-content.md)
      + [有循序追蹤的即時主要內容](sdk-implement/tracking-scenarios/live-sequential.md)
   + 驗證 {#validation}
      + [驗證總覽](sdk-implement/validation/validation-overview.md)
      + [測試 1：標準播放](sdk-implement/validation/test1-standard-playback.md)
      + [測試 2：媒體中斷](sdk-implement/validation/test2-media-interrupt.md)
      + [測試呼叫詳細資料](sdk-implement/validation/test-call-details.md)
      + [心率參數說明](sdk-implement/validation/heartbeat-params.md)
      + 偵錯 {#debugging}
         + [SDK 偵錯](sdk-implement/validation/debugging/sdk-debugging.md)
         + [設定 Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [建立新的 Debug 報表](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Debug 儀表板和報表](sdk-implement/validation/debugging/debug-dash-repts.md)
   + OTT 應用程式中的 Analytics {#analytics-with-ott}
      + [追蹤應用程式狀態](sdk-implement/analytics-with-ott/track-app-states.md)
      + [追蹤應用程式動作](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [設定使用者 ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT 與 Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT 與 Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + 逐步指南 {#cookbook}
      + [SDK 逐步指南](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [在播放期間處理應用程式中斷狀況](sdk-implement/cookbook/app-interrupts.md)
      + [解決 main:play 出現在廣告之間的問題](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [繼續非作用中工作階段](sdk-implement/cookbook/resuming-inactive.md)
      + [在 SceneGraph (Roku) 中進行追蹤](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + 從 Media Analytics 1.x 移轉至 2.x {#va-1x-to-2x}
      + [移轉總覽](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [程式碼比較：1.x 和 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [從 1.x 轉換為 2.x API](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK 移轉至 Launch {#sdk-to-launch}
      + [SDK 移轉至 Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK 移轉至 Launch 平台指南 {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [總覽](media-collection-api/mc-api-overview.md)
   + API 參考資料 {#mc-api-ref}
      + [工作階段要求](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [事件要求](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [要求參數](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [事件類型和說明](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON 驗證結構描述](media-collection-api/mc-api-ref/mc-api-json-validation.md)
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
   + 媒體追蹤時間軸 {#mc-api-timelines}
      + [時間軸 1 - 檢視到內容結尾](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [時間軸 2 - 使用者放棄工作階段](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [時間軸 3 - 章節](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ 逐步指南 {#media-analytics-cookbook}
   + [逐步指南](media-analytics-cookbook/media-analytics-cookbook.md)
   + [媒體串流歸因](media-analytics-cookbook/media-dimensions.md)
+ 量度和中繼資料 {#metrics-and-metadata}
   + [串流媒體參數](metrics-and-metadata/audio-video-parameters.md)
   + [廣告參數](metrics-and-metadata/ad-parameters.md)
   + [章節參數](metrics-and-metadata/chapter-parameters.md)
   + [播放器狀態參數](metrics-and-metadata/player-state-parameters.md)
   + [品質參數](metrics-and-metadata/quality-parameters.md)
   + [區段](metrics-and-metadata/segments.md)
   + [計算量度](metrics-and-metadata/calculated-metrics.md)
+ 報告與分析 {#media-reports}
   + [啟用媒體報表](media-reports/media-reports-enable.md)
   + 媒體預設報表 {#media-default-reports}
      + [預設報表總覽](media-reports/media-default-reports/default-reports-overview.md)
      + [媒體總覽](media-reports/media-default-reports/media-reports-overview.md)
      + [媒體詳細資料](media-reports/media-default-reports/media-reports-detail.md)
      + [媒體播出時段報表](media-reports/media-default-reports/media-reports-daypart.md)
      + [媒體同時檢閱者報表](media-reports/media-default-reports/media-concurrent-viewers.md)
   + 媒體工作區面板 {#media-workspace-panels}
      + [媒體同時檢閱者面板](media-reports/media-workspace-panels/media-concurrent-viewers.md)
      + [「媒體播放時間」面板](media-reports/media-workspace-panels/media-playback-time-spent.md)
   + [媒體工作區範本](media-reports/media-workspace-templates.md)
   + [透過 API 取得同時檢閱者資料](media-reports/media-default-reports/get-concurrent-json20.md)
   + [透過 API 取得媒體播放時間資料](media-reports/media-default-reports/get-mediaplaybacktimespent-json20.md)
+ [追蹤已下載的內容](media-collection-api/track-downloaded-content.md)
+ 播放器狀態追蹤 {#player-state-tracking}
   + [總覽](sdk-implement/player-state-tracking/player-state-overview.md)
   + [標準和自訂狀態](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [實作與報告](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [播放器狀態追蹤範例](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
+ 其他資源 {#additional-resources}
   + [發行說明](additional-resources/doc-updates.md)

<!-- + Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md)
-->
