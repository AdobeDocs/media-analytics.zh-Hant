---
title: 了解支援的裝置和平台
description: 「了解 Adobe Analytics for Streaming Media 所支援的主要裝置，例如 iOS、Android、OTT 裝置和 JavaScript 瀏覽器。」
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---

# 支援的裝置和平台 {#devices-supported}

>[!IMPORTANT]
>
>我們於 2021 年 8 月 31 日停止支援第 4 版 Mobile SDK 後，Adobe 也將停止支援 Media Analytics SDK iOS 版和 Android 版。如需詳細資訊，請參閱 [Media Analytics SDK 支援終止常見問題集](/help/sdk-implement/end-of-support-faqs.md)。

Adobe Analytics for Streaming Media 支援所有主要裝置，包括：

* iOS 和 Android 智慧型手機和平板電腦
* 適用於 ROKU、AppleTV、FireTV 以及 Android TV 的 OTT 裝置
* 適用於桌上型電腦和筆記型電腦的 JavaScript 瀏覽器

Media SDK 會因應裝置發佈新版本而定時更新，以便您能將 SDK 與目前大多數的大型媒體播放器整合，包括 Brightcove 和 Ooyala。

若是目前尚未支援 SDK 的裝置或平台，或您不想使用 SDK 的情況下，您可以選擇實作 Media Collection API。Media Collection API 可讓您直接從裝置或平台，對 Media Analytics 後端進行 RESTful API 呼叫。

目前支援的裝置和平台如下表所示。若要下載最新版 SDK，請參閱[下載 SDK](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html?lang=zh-Hant)。若裝置不在清單中，請連絡您的客戶服務人員或解決方案顧問，以瞭解該裝置的狀態。

| 串流平台和裝置 |  | 使用 AEP Mobile SDK 收集資料 | Media SDK | Media Collection API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| 網頁/行動網頁 |  |  |  |  |
|  | JavaScript 瀏覽器 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| 行動應用程式 |  |  |  |  |
|  | iOS 裝置 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android 裝置 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows 裝置 |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript) | ![](/help/assets/icon-blue-check.png)<br>(原生) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) |
|  | 遊戲主機 (例如 Xbox ONE、Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 機上盒 (例如 xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 智慧型電視 (例如 Samsung、LG、Sony、Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(Web 型) | ![](/help/assets/icon-blue-check.png) |
| 其他 |  |  |  |  |
|  | 新連網裝置 |  |  | ![](/help/assets/icon-blue-check.png) |

1. 我們將於 2021 年 8 月 31 日停止支援這些 SDK。如需詳細資訊，請參閱 [Media Analytics SDK 支援終止常見問題集](/help/sdk-implement/end-of-support-faqs.md)。

若要進一步了解各 SDK 的最低平台版本支援，請參閱[最低平台版本支援](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html?lang=zh-Hant)
