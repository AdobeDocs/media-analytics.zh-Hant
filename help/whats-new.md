---
title: Media Analytics 最新資訊
description: 最新資訊包括新功能和通知的相關資訊。
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '625'
ht-degree: 100%

---


# Media Analytics 最新資訊{#whats-new}

![橫幅](assets/media_analytics_banner.png)


此頁面主要說明 Media Analytics 的新功能、修正項目和重要注意事項。此外還有最新文件、訓練課程和教學課程影片，協助您充份運用 Media Analytics。


## 發行說明

Adobe Experience Cloud 發行說明

Adobe Experience Cloud 發行說明描述 Adobe Experience Cloud 的新功能、修正項目和重要注意事項。其中包括 Media Analytics 的最新變更。此外還有最新文件、訓練課程和教學課程影片，協助您充份運用 Experience Cloud。

## 新功能

| 功能 | [全面發佈](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=zh-Hant) - 目標日期 | 說明 |
| ----------- | ---------- | ---------- |
| [媒體同時檢閱者面板](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 2020 年 9 月 17 日 | 工作區的「媒體同時檢閱者」面板可供您掌握何時最多人同時觀看媒體，以及趨勢反轉的時間。這項功能提供內容品質和檢視者互動的重要分析，有助於疑難排解或依數量/規模完成規劃。 |
| [支援的裝置和平台](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=zh-Hant) | 2020 年 6 月 18 日 | 含 AEP Mobile SDK 的 [!UICONTROL Media Launch 擴充功能]現起支援下列 OTT 裝置：<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [播放器狀態追蹤](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html?lang=zh-Hant) | 2020 年 5 月 29 日 | [!UICONTROL Media Analytics] 客戶可使用全螢幕、隱藏式字幕、靜音、子母畫面和觀看中的標準解決方案變數集，擷取檢視者在播放時的互動。您也可以彈性建立自訂播放器狀態。[!UICONTROL Analysis Workspace] 中的報表現可使用[!UICONTROL 「播放器狀態追蹤」]變數。此功能需有下列任一個項目： <ul><li>Media [!DNL JavaScript] SDK 3.0 或更新版本</li><li>與 [!DNL Adobe Experience Platform] (AEP) SDK 搭配使用：</li><li>[!UICONTROL Media Analytics 擴充功能] (適用於網頁)：[!UICONTROL Adobe Media Analytics] (3.x SDK) for Audio and Video v1.0 或更新版本</li><li>[!UICONTROL Media Analytics 擴充功能] (適用於行動裝置)：[!UICONTROL Adobe Media Analytics for Audio] and Video v2.0 或更新版本</li><li>[!UICONTROL 媒體收集]</li></ul> |


## 重要通知

| 功能 | [全面發佈](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=zh-Hant) - 目標日期 | 說明 |
| ----------- | ---------- | ---------- |
| [支援的裝置和平台](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=zh-Hant) | 2021 年 8 月 31 日 | 我們於 2021 年 8 月 31 日停止支援第 4 版 Mobile SDK 後，Adobe 也將停止支援 Media Analytics SDK iOS 版和 Android 版。如需詳細資訊，請參閱 Media Analytics SDK 支援終止常見問題集。 |
| [Media Analytics SDK 支援終止常見問題集](sdk-implement/end-of-support-faqs.md) |   2019 年秋季 | 日後我們不會再開發 Media Analytics SDK iOS 版和 Android 版。從 2019 年秋季開始導入的新功能，會使用 Media Analytics 擴充功能和 Media Collection API 來啟用。 |
| [媒體概述](media-overview.md) | 2019 年 2 月 20 日 | Adobe 僅支援 TLS 1.1 或更新版本。經過這項變更後，Adobe 將不再從使用較舊裝置或部署 TLS 1.0 之網頁瀏覽器的使用者收集資料。 |
| [支援的裝置和平台](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=zh-Hant) | 2019 年 2 月 19 日 | 以下列出各 SDK 的最低平台版本支援。<br>- iOS：iOS 6+ <br>- Android：Android 5.0+ - Lollipop <br>-  Chrome：v22+<br>- Mozilla：v27+<br>- Safari：v7+<br>- IE：v1+ |
| [音訊和視訊參數](metrics-and-metadata/audio-video-parameters.md) | 2019 年 2 月 7 日 | Adobe Analytics for Video and Audio 發佈了量度名稱變更。<i>媒體起始</i>將更名為<i>媒體開始次數</i>。做出這項變更是為了反映量度和報告的業界標準，並讓量度在報告中易於識別。 |
| [音訊和視訊參數](metrics-and-metadata/audio-video-parameters.md) | 2018 年 9 月 13 日 | 我們變更了某些維度、量度與報表的標籤，以便交叉追蹤 Video Analytics 與 Audio Analytics 的內容。變更的標籤包括：*視訊起始*&#x200B;變更為&#x200B;*媒體起始*、*視訊長度*&#x200B;變更為&#x200B;*內容長度*、*視訊名稱*&#x200B;變更為&#x200B;*內容名稱*。Reports and Analytics 中的視訊報表已全數更新，捨棄「視訊」一名而改用「媒體」。標籤變更並未改變資料收集或歷史資料。如果您要在 Report Builder 或其他任何受到前述變更影響的外部自動化資料提取中使用這些標籤，請多加留意。 |




<!-- | title | date | description | -->
