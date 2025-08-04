---
title: 串流媒體收集發行說明
description: 檢視串流媒體收集發行說明的發行說明。
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 70%

---

# 串流媒體收集發行說明（2023年5月）

**上次更新日期**： 2024年5月29日

## 相關資源

有關針對管理員的新功能、修正和重要資訊的資訊，請參閱以下資源。

* [Adobe Analytics 發行說明](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=zh-Hant)
* [Customer Journey Analytics 發行說明](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=zh-Hant)
* [Adobe Experience Cloud 產品](https://business.adobe.com/products/adobe-experience-cloud-products.html)的最新版更新。

* [Adobe Analytics 教學課程](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=zh-Hant)

## *最新發行說明*

## Adobe串流媒體集合中的新功能和更新功能 {#cja-features}

| 功能 | 說明 | 目標日期 |
| ----------- | ---------- | ------- |
| 已更新 XDM 欄位，可將串流媒體資料收集到 Adobe Experience Platform | 將串流媒體資料收集至 Adobe Experience Platform 時，不應再使用串流媒體參數文件中「XDM 欄位路徑」標題下顯示的 XDM 欄位路徑。反之，在2025年5月9日之前實作Analytics來源聯結器以收集串流媒體資料至Platform的客戶必須將其現有設定移轉至mediaReporting欄位路徑，如串流媒體引數檔案的「報告XDM欄位路徑」標題下所示。<p> 這些欄位路徑可在下列頁面上找到，並標示為「已棄用」： [音訊和視訊引數](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/implementation/variables/audio-video-parameters)、[廣告引數](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/implementation/variables/ad-parameters)、[章節引數](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/implementation/variables/chapter-parameters)、[播放器狀態引數](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/implementation/variables/player-state-parameters)以及[品質引數](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/implementation/variables/quality-parameters)。 （在2025年5月9日之後實施Analytics來源聯結器，而且已經只使用mediaReporting XDM路徑的客戶不需要採取任何動作。）</p><p>淘汰XDM欄位路徑上的資料內嵌將持續到2025年10月底。 之後，已棄用的欄位路徑將完全移除，不再顯示於Adobe Experience Platform結構描述UI中，而且只會使用mediaReporting欄位路徑傳送資料。</p><p>如需詳細資訊，請參閱[將Analytics Source Connector實作移轉至更新的XDM串流媒體欄位](/help/use-cases/xdm-updates/updated-xdm-fields.md)。</p><p>如需移轉支援，請聯絡您的Adobe Consulting服務或帳戶團隊。 </p> | 2025 年 10 月 |
| 使用網頁SDK將網頁資料傳送至Adobe Experience Platform Edge Network | 您現在可以[使用Adobe Experience Platform Web SDK將串流媒體網頁資料傳送至Adobe Experience Platform Edge Network](/help/implementation/edge/edge-web-sdk.md)，讓您建立更個人化的行銷活動並提供更個人化的內容，產生更多可報告的追蹤資料。<p>此增強功能可為所有平台解決方案 (例如 Customer Journey Analytics、RT-CDP、AJO 和事件轉送) 的 Web 實作提供統一的資料收集方法。以前，將串流媒體 Web 資料傳送到 Edge Network 時，唯一的方法就是使用 Media Edge API。 | 2024 年 5 月 29 日 |
| 將Roku資料傳送至Adobe Experience Platform Edge | 現在，[透過 Experience Platform Edge 安裝串流媒體收集](/help/implementation/edge/implementation-edge.md)時，您可以使用 Adobe Experience Platform Roku SDK 將串流媒體資料傳送至 Adobe Experience Platform。 | 2024 年 4 月 12 日 |
| 媒體收集：與Experience Edge (API和Mobile SDK)整合 | 您現在可以使用Experience Edge API和Mobile SDK來實作Adobe串流媒體收集，好讓您可以建立更個人化的行銷活動並提供更個人化的內容，進而產生更多可報告的追蹤資料。<p>此增強功能提供跨所有解決方案的統一收集方法，例如Customer Journey Analytics報告、RT-CDP、AJO和事件轉送。  [了解更多](/help/implementation/edge/implementation-edge.md) | 2023年5月12日 |
| 「媒體同時檢閱者」面板 | 了解高峰期同時觀看或使用者數下降的位置。 取得內容品質和檢閱者參與的寶貴見解，並取得疑難排解或規劃數量和規模的協助。 [了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=zh-Hant) | 2022 年 8 月 9 日 |
| 「媒體播放時間」面板 | 「媒體播放時間」提供寶貴的對象參與度深入分析，並可讓媒體組織透過進階花費時間分析及日時段分割功能，取得更深入、更細微的分析並包含每分鐘的使用者參與度。 您可以觀察使用者在特定時間點觀看您的媒體串流所花的時間多寡。 您可以依不同的資料粒度 (包括新的 5 分鐘、15 分鐘和 30 分鐘資料粒度) 分割播放持續時間。[了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=zh-Hant) | 2022 年 8 月 9 日 |
| 在行動計分卡上分享註解 | 您可以在行動計分卡上顯示建立於工作區的註解。如此，您就可以直接在行動計分卡專案上分享組織和活動相關的資料細微差別和深入解析，此類專案可在 Analytics 儀表板行動應用程式中檢視。[了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=zh-Hant) | 2022 年 6 月 15 日 |
| 適用於 Customer Journey Analytics 的 Report Builder 更新內容 | 包含像是排程和資料區塊管理員等功能。 [了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=zh-Hant) | 2022 年 5 月 18 日 |
| 工作區中的註解 | 工作區中的註解讓您能夠有效地將內容相關的資料細微差別和深入解析傳達給您的組織。[了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=zh-Hant) | 逐步推出於 2022 年 3 月 23 日開始 |
| 行動計分卡專案預覽模式 | 直接從計分卡產生器中的 Analytics 儀表板應用程式啟動行動計分卡的外觀預覽。預覽模式可讓使用者透過與應用程式相同的方式來與篩選器和圖表互動，在儲存和共用計分卡之前先預覽體驗。使用者還可以在預覽模式下使用裝置選擇器來查看不同裝置上的計分卡外觀。[了解更多](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=zh-Hant#preview) | 2022 年 2 月 16 日 |


## Adobe串流媒體集合中的新功能和更新功能 {#sm-features}

| 功能 | 說明 | 目標日期 |
| ----------- | ---------- | ------- |
| 多播放器狀態追蹤 | 使用 Media Collection API 來實施多播放器狀態追蹤。 [了解更多](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=zh-Hant) | 2022 年 9 月 |
| 已重新命名 XDM 欄位 | 已重新命名 XDM 欄位名稱以保持一致性：<br>* 音訊和視訊參數<br>* 廣告參數<br>* 章節參數<br>* 播放器狀態參數<br>* 品質參數 | 2022 年 9 月 |
| Device Co-op 參考 | 已移除 Adobe Experience Cloud Device Co-op 和 Experience Cloud ID 服務需求。 | 2022 年 8 月 |
| 已更新用於收集和報告的欄位名稱和 XDM 路徑 | 已更新以下項目：<br>* 音訊和視訊參數<br>* 廣告參數<br>* 章節參數<br>* 播放器狀態參數<br>* 品質參數 | 2022 年 8 月 |
| 平均分鐘觀眾數 | Media Analytics 客戶可以使用「平均分鐘觀眾數」面板來更了解平均內容使用量。<br>「平均分鐘觀眾數」可比較任何長度或類型的節目。此外，您也可以比較數位平均分鐘觀眾數和線性電視的平均分鐘量度，或是將前者附加到後者。此面板提供較大的彈性來測量自訂時段的平均觀眾數，以及持續時間分類的更新時間。[了解更多](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=zh-Hant) | 2022 年 3 月 16 日 |
| 媒體播放時間面板 | 了解媒體播放時間花費面板如何透過一天中所選粒度期間的觀看時間，來讓媒體用戶了解他們的觀看量。<br>[「媒體播放逗留時間」面板 (教學課程)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=zh-Hant) | 2022 年 1 月 |


## *舊版發行說明*

| 功能 | 說明 | 目標或更新日期 |
| ----------- | ---------- | -------------- |
| 媒體播放時間 | Adobe 串流媒體播放時間提供寶貴的對象參與度深入分析，並可讓媒體組織透過進階花費時間分析及時段功能，以每分鐘的使用者參與度取得更深入、更細微的分析。您可以觀察在特定時間點觀看您的媒體串流所花費的時間多寡。您可以依不同的資料粒度 (包括新的 5 分鐘、15 分鐘和 30 分鐘資料粒度) 分割播放持續時間。 [了解更多...](/help/reporting/workspace/media-playback-time-spent.md) | 2021 年 9 月 |
| Analytics Workspace 中的「媒體同時檢閱者」面板 | 了解高峰期同時觀看或使用者數下降的位置。 取得內容品質和檢閱者參與的寶貴見解，並取得疑難排解或規劃數量和規模的協助。 [了解更多…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspace 中的「媒體同時檢閱者」面板 (教學課程)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=zh-Hant#analysis-workspace) | 2020 年 9 月<br><br><br>2021 年 1 月 |
| 支援的裝置和平台 | 含 AEP SDK 的 Media Launch 擴充功能現在支援下列 OTT 裝置： <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020 年 6 月 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
