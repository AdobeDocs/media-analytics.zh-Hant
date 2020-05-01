---
title: 支援的裝置
description: null
uuid: null
translation-type: tm+mt
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8

---


# 支援的裝置 {#devices-supported}

Adobe Analytics for Audio and Video可確保在所有裝置上收集和報告每個媒體串流。

Adobe Analytics for Audio and Video支援所有主要裝置，包括：

* iOS 和 Android 智慧型手機和平板電腦
* 適用於 ROKU、AppleTV、FireTV 以及 Android TV 的 OTT 裝置
* 適用於桌上型電腦和筆記型電腦的 JavaScript 瀏覽器

當新版裝置發行時，Media SDK會定期更新，而您可使用SDK與現今最大型的媒體播放器整合，包括Brightcove和Ooyala。

對於目前沒有SDK支援的裝置或平台，或您不想使用SDK的情況，您可以實作Media Collection API。 Media Collection API可讓您直接從裝置或平台對Media Analytics後端進行REST風格的API呼叫。

下表列出目前支援的裝置。 若要下載最新版 SDK，請參閱[下載 SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)。如果未列出裝置，請連絡您的客戶服務或解決方案顧問以取得該裝置的狀態。


| 串流平台／裝置 |  | 使用AEP SDK的Media Launch Extension | Media SDK | 媒體收集 API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| 網頁／行動網路 |  |  |  |  |
|  | JavaScript瀏覽器 | X | X | X |
| 行動應用程式 |  |  |  |  |
|  | iOS 裝置 | X | X | X |
|  | Android 裝置 | X | X | X |
|  | Windows裝置 |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV（舊版、TVOS） |  | X | X |
|  | 羅庫 |  | X<br>(BrightScript) | X<br>（原生） |
|  | Fire TV(Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | 遊戲主機（例如Xbox ONE、Sony PS3/PS4） |  |  | X |
|  | 機上盒（例如xfinity X1） |  |  | X |
|  | 智慧型電視（例如Samsung、LG、Sony、Vizio） |  | X<br>（基於Web） | X |
| 其他 |  |  |  |  |
|  | 全新連接的裝置 |  |  | X |


若為 Media SDK，請另行參閱[最低平台版本支援](./sdk-implement/setup/setup-overview.md#minimum-platform-version)
