---
title: 存取下載 Media Analytics SDK 的連結
description: 各平台適用的 SDK 下載內容連結，包括 Android、iOS、JavaScript、Chromecast 和 Roku。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 81%

---

# 取得 Media SDK、使用標記的擴充功能和 OTT SDK {#download-sdks}

本頁資訊包含下載最新 Media SDK 以及取得使用標記的 Media 擴充功能的連結。

Adobe Experience Platform 中的標記是 Adobe 推出的新一代網站標記與 Mobile SDK 管理功能。標記提供一種簡單的方式來部署及管理所有必要的分析、行銷及廣告解決方案，以便支援相關客戶體驗。如需關於標記的其他資訊，請參閱[標記概觀](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=zh-Hant).


>[!NOTE]
>
>如需有關下載舊版 SDK 的資訊，請參閱[舊版 — 下載 SDK](/help/legacy/legacy-download-sdks.md)。<br>
>如需關於終止支援的重要資訊，請參閱[終止支援常見問題集](/help/additional-resources/end-of-support-faqs.md)。

## Media SDK 和行動程式庫 {#media-sdks-libraries}

### Web 實作 {#download-web-sdk}

| 支援的平台 | 支援的解決方案 | 實作方法 |  版本 |  API   |  文件 |  範例  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript圖示&#x200B;](assets/javascript-icon.png)</br>**JAVASCRIPT API** | Adobe Analytics | 僅限 Analytics | Web - [JS 適用的 Media SDK v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [使用JavaScript安裝Media SDK](/help/implementation/media-sdk/setup/web-implementation.md) | [JS 適用的 Media SDK v3.0.2 範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript圖示&#x200B;](assets/javascript-icon.png)</br>**JAVASCRIPT API** | Adobe Analytics | 僅限 Analytics | Web - Media 擴充功能 |  | [Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能 — 使用標記 (資料收集)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant) | [Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | 網頁 — Experience PlatformEdge |  | [使用Edge Network實作串流媒體收集附加元件](/help/implementation/edge/implementation-edge.md) <p>與</p><p>[使用Adobe Experience Platform Web SDK傳送Web資料至Edge](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobile 實施 {#get-mobile-extension}

| 支援的平台 | 支援的解決方案 | 實作方法 |  版本 |  文件   |  範例  |
|:---:|---|---|---|---|---|
| ![Android圖示&#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | 僅限 Analytics | Android - Media 擴充功能 | [Mobile SDK 文件](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS 圖示&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | 僅限 Analytics | iOS/tvOS - Media 擴充功能 | [Mobile SDK 文件](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 範例](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android圖示&#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS 圖示&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) |  |

### 過頂實作 {#download-ott-libraries}

| 支援的平台 | 支援的解決方案 | 實作方法 |  版本 |  API   |  文件 |
|:---:|---|---|---|---|---|
| ![Chromecast圖示&#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | 僅限 Analytics | [Chromecast 適用的 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [設定 Chromecast 適用的 Mobile SDK v3.x](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku圖示&#x200B;](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | 僅限 Analytics | [Roku 適用的 SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [設定 Roku 適用的 Mobile SDK v2.x](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku圖示&#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) |
