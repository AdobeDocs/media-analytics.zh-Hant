---
title: 取得Media SDK、擴充功能和API
description: 各平台適用的 SDK 下載內容連結，包括 Android、iOS、JavaScript、Chromecast 和 Roku。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 575
ht-degree: 32%

---

# 取得Media SDK、擴充功能和API

## Edge實施（建議） {#edge-sdks}

Edge實施作業會收集資料一次，並透過Adobe Experience Platform Edge Network傳送資料至多個目的地：Adobe Analytics、Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP。 對於沒有原生SDK的平台（例如智慧型電視、遊戲機和機上盒），請使用Media Edge API。

| | 文件 | 範例 |
|:---:|---|---|
| [![JavaScript圖示](assets/javascript-icon.png)](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/install/overview)<br>[網頁SDK](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/install/overview) | [設定適用於串流媒體的Web SDK](/help/implementation/edge/web-sdk.md) | [樣本](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![擴充功能圖示](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=zh-Hant)<br>[Web SDK標籤擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=zh-Hant) | [設定適用於串流媒體的Web SDK標籤延伸模組](/help/implementation/edge/web-sdk-tags.md) | [樣本](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Android圖示](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [設定適用於串流媒體的Android](/help/implementation/edge/android.md) | [樣本](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Apple iOS圖示](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [設定適用於串流媒體的iOS](/help/implementation/edge/ios.md) | [樣本](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![擴充功能圖示](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Android標籤擴充功能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [設定適用於串流媒體的Android標籤延伸模組](/help/implementation/edge/android-tags.md) | |
| [![擴充功能圖示](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[iOS / tvOS標籤擴充功能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [設定適用於串流媒體的iOS標籤延伸模組](/help/implementation/edge/ios-tags.md) | |
| [![Roku圖示](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku SDK](https://github.com/adobe/aepsdk-roku) | [設定適用於串流媒體的Roku](/help/implementation/edge/roku.md) | [樣本](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![API圖示](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[Media Edge API](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [設定Media Edge API](/help/implementation/edge/media-edge-api.md) | [樣本](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## 僅限Analytics的實作 {#analytics-only-sdks}

這些SDK和擴充功能會直接將資料傳送至Adobe Analytics。 若為新實作，請使用上述Edge實作。 若要將現有的Analytics資料帶入Customer Journey Analytics或其他Experience Platform應用程式，請使用[Analytics來源聯結器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)。

| | 文件 | 範例 |
|:---:|---|---|
| [![JavaScript圖示](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [設定適用於串流媒體的JavaScript](/help/implementation/analytics-only/javascript.md) | [樣本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![擴充功能圖示](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant)<br>[媒體擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant) | [使用串流媒體的標籤設定JavaScript](/help/implementation/analytics-only/javascript-tags.md) | [樣本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Chromecast圖示](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [設定適用於串流媒體的Chromecast](/help/implementation/analytics-only/chromecast.md) | [樣本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![API圖示](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[媒體收集API](/help/implementation/media-collection-api/mc-api-overview.md) | [設定Media Collection API](/help/implementation/analytics-only/media-collection-api.md) | |
