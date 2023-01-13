---
product: adobe analytics
audience: end-user
user-guide-title: 適用於串流媒體的 Adobe Analytics
breadcrumb-title: Media Analytics 指南
user-guide-description: 實作適用於串流媒體的 Adobe Analytics。包含 Media SDK 和 Media Collection API。
sub-product: media analytics
source-git-commit: 5c0195ab6945b65cd37f2e8fd9ddc8c8e91507f0
workflow-type: ht
source-wordcount: '895'
ht-degree: 100%

---


# 適用於串流媒體的 Adobe Analytics {#using}

+ [適用於串流媒體的 Analytics 指南](media-overview.md)
+ 發行說明 {#release-notes}
   + [串流媒體發行說明](additional-resources/release-notes.md)
+ 快速入門 {#getting-started}
   + [概觀](getting-started/getting-started.md)
   + [先決條件](getting-started/prereqs.md)
   + [支援裝置](getting-started/supported-devices.md)
   + [串流媒體文件](getting-started/implementation-documentation.md)
   + [SDK、程式庫與擴充功能](getting-started/download-sdks.md)
   + 終止支援 {#end-of-support}
      + [Media Analytics Mobile SDK 終止支援](additional-resources/end-of-support-faqs.md)
      + 舊版 - 獨立 Media SDK 移轉至 Launch {#sdk-to-launch}
         + [概觀](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - Media SDK 至 Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - Media SDK 至 Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - Media SDK 至 Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ 實作{#implementation}
   + [實作概觀](implementation/overview.md)
   + Media SDK - 實作{#media-sdk}
      + [Media SDK 概觀](implementation/media-sdk/media-sdk-overview.md)
      + 安裝與設定 {#setup}
         + 安裝 Web SDK {#install-web-sdk}
            + [使用 JavaScript 安裝 Analytics](implementation/media-sdk/setup/web-implementation.md)
            + [使用 Media Analytics 擴充功能安裝 Analytics](implementation/media-sdk/setup/web-implementation-tags.md)
         + [安裝 Mobile SDK](implementation/media-sdk/setup/mobile-implementation.md)
         + 安裝 OTT SDK {#ott-setup}
            + [安裝 Chromecast SDK](implementation/media-sdk/setup/set-up-chromecast.md)
            + [安裝 Roku SDK](implementation/media-sdk/setup/set-up-roku.md)
   + Media Collection API- 實作{#streaming-media-apis}
      + [媒體收集](implementation/media-collection-api/mc-api-overview.md)
      + [API 快速入門](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [工作階段要求](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [事件要求](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [要求參數](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [事件類型和說明](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
      + 實作 API {#mc-api-impl}
         + [在播放器中設定 HTTP 要求類型](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
         + [取得工作階段 ID](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
         + [實作事件要求](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
         + [JSON 驗證結構](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
         + [驗證事件要求](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
         + [傳送 Ping 事件](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
         + [傳送 QoE 資料](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
         + [自訂中繼資料支援](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
         + [逾時條件](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
         + [控制事件順序](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
         + [在工作階段回應緩慢時將事件加入佇列](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 變數 {#variables}
      + [串流媒體參數](implementation/variables/audio-video-parameters.md)
      + [廣告參數](implementation/variables/ad-parameters.md)
      + [章節參數](implementation/variables/chapter-parameters.md)
      + [播放器狀態參數](implementation/variables/player-state-parameters.md)
      + [品質參數](implementation/variables/quality-parameters.md)
      + [計算量度](implementation/variables/calculated-metrics.md)
+ 報表 {#media-reports}
   + [啟用媒體報表](reporting/media-reports-enable.md)
   + [關於區段](reporting/segments.md)
   + 媒體預設報表 {#media-default-reports}
      + [預設報表概觀](reporting/reports-and-analytics/default-reports-overview.md)
      + [媒體概觀](reporting/reports-and-analytics/media-reports-overview.md)
      + [媒體詳細資料](reporting/reports-and-analytics/media-reports-detail.md)
      + [媒體播出時段報表](reporting/reports-and-analytics/media-reports-daypart.md)
      + [媒體同時檢閱者報表](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + 媒體工作區面板 {#media-workspace-panels}
      + [「媒體平均每分鐘對象數」面板](reporting/workspace/average-minute-audience.md)
      + [「媒體同時檢閱者」面板](reporting/workspace/media-concurrent-viewers-overview.md)
      + [「媒體播放時間」面板](reporting/workspace/media-playback-time-spent.md)
   + [媒體工作區範本](reporting/workspace/media-workspace-templates.md)
   + [透過 API 取得同時檢閱者資料](reporting/reports-and-analytics/get-concurrent-json20.md)
   + [透過 API 取得媒體播放時間資料](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ 使用案例 {#media-use-cases}
   + [Media SDK 使用案例 ](use-cases/cookbook/sdk-cookbook-overview.md)
   + 播放器狀態追蹤 {#player-state-tracking}
      + [概觀](use-cases/player-state-tracking/player-state-overview.md)
      + [標準和自訂狀態](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [實作與報告](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [多播放器狀態追蹤](use-cases/player-state-tracking/multiple-player-states.md)
      + [播放器狀態追蹤範例](use-cases/player-state-tracking/player-state-examples.md)
   + [追蹤離線下載的內容](use-cases/track-downloaded-content.md)
   + [Federated Analytics](use-cases/federated-analytics.md)
   + [在播放期間處理應用程式中斷狀況](use-cases/cookbook/app-interrupts.md)
   + [媒體串流歸因](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [繼續非作用中工作階段](use-cases/cookbook/resuming-inactive.md)
   + [使用 SceneGraph 在 Roku 進行追蹤](use-cases/cookbook/sdk-track-scenegraph.md)
   + [處理廣告之間的差距](use-cases/cookbook/fix-ad-play-ad.md)
   + 時間軸 {#timelines}
      + [章節開始和結束](use-cases/timelines/chapter-start-end.md)
      + [檢視到內容結束](use-cases/timelines/view-to-end-of-content.md)
      + [捨棄工作階段](use-cases/timelines/user-abandons-session.md)
   + 在 OTT 應用程式中使用 Analytics {#analytics-with-ott}
      + [追蹤應用程式狀態](use-cases/analytics-with-ott/track-app-states.md)
      + [追蹤應用程式動作](use-cases/analytics-with-ott/track-app-actions.md)
      + [設定使用者 ID](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT 與 Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT 與 Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ 追蹤 {#tracking}
   + 追蹤 {#track-av-playback}
      + [概觀](use-cases/track-av-playback/track-core-overview.md)
      + 追蹤核心串流媒體播放 {#track-core}
         + [在 JavaScript 3.x 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [在 Chromecast 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-chromecast.md)
         + [在 Roku 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-roku.md)
      + 追蹤緩衝 {#track-buffering}
         + [在 JavaScript 3.x 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [在 Chromecast 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在 Roku 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
      + 追蹤搜尋 {#track-seeking}
         + [在 JavaScript 3.x 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [在 Chromecast 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [在 Roku 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
      + 實作標準中繼資料 {#impl-std-metadata}
         + [在 JavaScript 3.x 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [在 Chromecast 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [標準中繼資料參數 - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [標準中繼資料參數 - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
      + 追蹤廣告 {#track-ads}
         + [概觀](use-cases/track-ads/track-ads-overview.md)
         + [在 JavaScript 3.x 上追蹤廣告](use-cases/track-ads/track-ads-js/track-ads-js3.md)
         + [在 Chromecast 上追蹤廣告](use-cases/track-ads/track-ads-chromecast.md)
         + [在 Roku 上追蹤廣告](use-cases/track-ads/track-ads-roku.md)
         + 實作標準廣告中繼資料 {#impl-std-ad-metadata}
            + [在 JavaScript 3.x 上實作標準廣告中繼資料](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
            + [在 Roku 上實作標準廣告中繼資料](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
      + 追蹤章節和區段 {#track-chapters}
         + [概觀](use-cases/track-chapters/track-chapters-overview.md)
         + [在 JavaScript 3.x 上追蹤章節和區段](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
         + [在 Chromecast 上追蹤章節和區段](use-cases/track-chapters/track-chapters-chromecast.md)
         + [在 Roku 上追蹤章節和區段](use-cases/track-chapters/track-chapters-roku.md)
      + 追蹤體驗品質 {#track-qos}
         + [概觀](use-cases/track-qos/track-qos-overview.md)
         + [在 JavaScript 3.x 上追蹤體驗品質](use-cases/track-qos/track-qos-js/track-qos-js3.md)
         + [在 Chromecast 上追蹤體驗品質](use-cases/track-qos/track-qos-chromecast.md)
         + [在 Roku 上追蹤體驗品質](use-cases/track-qos/track-qos-roku.md)
      + 追蹤錯誤 {#track-errors}
         + [概觀](use-cases/track-errors/track-errors-overview.md)
         + [在 JavaScript 3.x 上追蹤錯誤](use-cases/track-errors/track-errors-js/track-errors-js3.md)
         + [在 Chromecast 上追蹤錯誤](use-cases/track-errors/track-errors-chromecast.md)
         + [在 Roku 上追蹤錯誤](use-cases/track-errors/track-errors-roku.md)
+ 隱私權與安全性 {#streaming-media-privacy}
   + [選擇退出與隱私權設定](privacy/opt-out-privacy.md)
   + [安全性](privacy/security.md)
+ 舊版實作 {#legacy-implementations}
   + [舊版 - 概觀](legacy/setup/legacy-setup-overview.md)
   + [舊版 — 下載 SDK](legacy/legacy-download-sdks.md)
   + 舊版 - Media SDK{#legacy-media-sdks}
      + [舊版 - Media SDK 概觀](legacy/media-sdk/setup/setup-overview.md)
      + [設定 Android](legacy/media-sdk/setup/set-up-android.md)
      + [設定 iOS](legacy/media-sdk/setup/set-up-ios.md)
      + 設定 JavaScript {#setup-javascript}
         + [設定 JavaScript 3.x](legacy/media-sdk/setup/setup-javascript/set-up-js-3.md)
   + [關於心率測量](legacy/heartbeat-measurement.md)
   + [Adobe Primetime 和適用於串流媒體的 Analytics](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe Audience Management 啟用](legacy/intro-to-ava/am-enablement.md)
   + [自訂連結實作](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + 舊版里程碑追蹤 {#legacy-milestone-tracking}
      + [舊版里程碑追蹤](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [將里程碑移轉到 VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [將里程碑移轉到 CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + 驗證 {#validation}
      + [驗證概觀](legacy/validation/validation-overview.md)
      + [測試 1：標準播放](legacy/validation/test1-standard-playback.md)
      + [測試 2：媒體中斷](legacy/validation/test2-media-interrupt.md)
      + [測試呼叫詳細資料](legacy/validation/test-call-details.md)
      + [心率參數說明](legacy/validation/heartbeat-params.md)
      + 偵錯 {#debugging}
         + [SDK 偵錯](legacy/validation/debugging/sdk-debugging.md)
   + [舊版移轉： VHL 1.x 至 VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [設定 JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [程式碼比較： v1.x 與 v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [追蹤 API 1x 至 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [舊版 - AVA 介紹](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [用戶端路徑](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + 舊版追蹤 {#track-av-playback}
      + [在 Android 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-android.md)
      + [在 iOS 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-ios.md)
      + 在 JavaScript 上追蹤核心播放 {#track-core-javascript}
         + [在 JavaScript 2.x 上追蹤核心播放](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
      + [在 Android 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
      + [在 iOS 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
      + 在 JavaScript 上追蹤緩衝 {#track-buffering-js}
         + [在 JavaScript 2.x 上追蹤緩衝](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
      + [在 Android 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
      + [在 iOS 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
      + 在 JavaScript 上追蹤搜尋 {#track-seeking-js}
         + [在 JavaScript 2.x 上追蹤搜尋](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
      + [在 Android 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
      + [在 iOS 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      + [iOS 中繼資料索引鍵](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
      + 在 JavaScript 上實作標準中繼資料 {#impl-std-md-js}
         + [在 JavaScript 2.x 上實作標準中繼資料](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + 追蹤廣告 {#track-ads}
         + [在 Android 上追蹤廣告](use-cases/track-ads/track-ads-android.md)
         + [在 iOS 上追蹤廣告](use-cases/track-ads/track-ads-ios.md)
         + 在 JavaScript 上追蹤廣告 {#track-ads-js}
            + [在 JavaScript 2.x 上追蹤廣告](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [在 Android 上實作標準廣告中繼資料](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [在 iOS 上實作標準廣告中繼資料](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + 在 JavaScript 上實作標準廣告中繼資料 {#impl-std-ad-md-js}
               + [在 JavaScript 2.x 上實作標準廣告中繼資料](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + 追蹤章節和區段 {#track-chapters}
         + [在 Android 上追蹤章節和區段](use-cases/track-chapters/track-chapters-android.md)
         + [在 iOS 上追蹤章節和區段](use-cases/track-chapters/track-chapters-ios.md)
         + 在 JavaScript 上追蹤章節和區段 {#track-chapters-js}
            + [在 JavaScript 2.x 上追蹤章節和區段](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [在 Android 上追蹤體驗品質](use-cases/track-qos/track-qos-android.md)
         + [在 iOS 上追蹤體驗品質](use-cases/track-qos/track-qos-ios.md)
         + 在 JavaScript 上追蹤體驗品質 {#track-qos-js}
            + [在 JavaScript 2.x 上追蹤體驗品質](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + 追蹤錯誤 {#track-errors}
         + [在 Android 上追蹤錯誤](use-cases/track-errors/track-errors-android.md)
         + [在 iOS 上追蹤錯誤](use-cases/track-errors/track-errors-ios.md)
         + 在 JavaScript 上追蹤錯誤 {#track-errors-js}
            + [在 JavaScript 2.x 上追蹤錯誤](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + 追蹤案例 {#tracking-scenarios}
         + [沒有廣告的 VOD 播放](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [有前段廣告的 VOD 播放](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [已略過廣告的 VOD 播放](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [有一個章節的 VOD 播放](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [已略過章節的 VOD 播放](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [主要內容中具有搜尋功能的 VOD 播放](use-cases/tracking-scenarios/vod-seeking.md)
         + [有緩衝的 VOD 播放](use-cases/tracking-scenarios/vod-buffering.md)
         + [多個 VOD 追蹤器並行](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [用於多個工作階段的一個 VOD 追蹤器](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [即時主要內容](use-cases/tracking-scenarios/live-main-content.md)
         + [有循序追蹤的即時主要內容](use-cases/tracking-scenarios/live-sequential.md)
