---
title: 存取下載 Media Analytics SDK 的連結
description: 各平台適用的 SDK 下載內容連結，包括 Android、iOS、JavaScript、Chromecast 和 Roku。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 84%

---

# 取得 Media SDK、使用標記的擴充功能和 OTT SDK {#download-sdks}

本頁資訊包含下載最新 Media SDK 以及取得使用標記的 Media 擴充功能的連結。

Adobe Experience Platform 中的標記是 Adobe 推出的新一代網站標記與 Mobile SDK 管理功能。 標記提供一種簡單的方式來部署及管理所有必要的分析、行銷及廣告解決方案，以便支援相關客戶體驗。 如需關於標記的其他資訊，請參閱[標記概觀](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=zh-Hant).


>[!NOTE]
>
>如需有關下載舊版SDK的資訊，請參閱[舊版 — 下載SDK](/help/legacy/legacy-download-sdks.md)。<br>
>如需關於終止支援的重要資訊，請參閱[終止支援常見問題集](/help/additional-resources/end-of-support-faqs.md)。

## Media SDK 和行動程式庫 {#media-sdks-libraries}

### Web 實作 {#download-web-sdk}

| 支援的平台 | 支援的解決方案 | 實作方法 | 版本 |  API   |  文件  |  範例  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript圖示&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | 僅限 Analytics | Web - [JS 適用的 Media SDK v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [使用JavaScript安裝Media SDK](/help/implementation/media-sdk/setup/web-implementation.md) | [JS 適用的 Media SDK v3.0.2 範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript圖示&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | 僅限 Analytics | Web - Media 擴充功能 |  | [Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能 — 使用標記 (資料收集)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant) | [Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | 網路 — Experience Platform Edge |  | [使用Edge Network實作Customer Journey Analytics串流媒體集合](/help/implementation/edge/implementation-edge.md) <p>和</p><p>[使用Adobe Experience Platform Web SDK將網頁資料傳送至Edge](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobile 實施 {#get-mobile-extension}

| 支援的平台 | 支援的解決方案 | 實作方法 | 版本 |  文件   |  範例  |
|:---:|---|---|---|---|---|
| ![Android圖示&#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | 僅限 Analytics | Android - Media 擴充功能 | [Mobile SDK 文件](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 範例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS 圖示&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | 僅限 Analytics | iOS/tvOS - Media 擴充功能 | [Mobile SDK 文件](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 範例](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android圖示&#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS 圖示&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) |  |

### 過頂實作 {#download-ott-libraries}

| 支援的平台 | 支援的解決方案 | 實作方法 | 版本 |  API   |  文件  |
|:---:|---|---|---|---|---|
| ![Chromecast圖示&#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | 僅限 Analytics | [Chromecast 適用的 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [設定 Chromecast 適用的 Mobile SDK v3.x](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku圖示&#x200B;](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | 僅限 Analytics | [Roku 適用的 SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [設定 Roku 適用的 Mobile SDK v2.x](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku圖示&#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [使用JavaScript安裝Media SDK](/help/implementation/edge/implementation-edge.md) |
