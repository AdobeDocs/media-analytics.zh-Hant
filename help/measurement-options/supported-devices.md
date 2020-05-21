---
title: 支援的裝置和平台
description: Adobe Analytics for Audio and Video可確保在所有裝置上收集和報告每個媒體串流。
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# 支援的裝置和平台 {#devices-supported}

>[!IMPORTANT]
>
>在2021年8月31日終止對第4版行動SDK的支援後，Adobe也將終止對iOS和Android專用Media Analytics SDK的支援。  如需詳細資訊，請 [參閱「媒體分析SDK終止支援常見問答」](/help/sdk-implement/end-of-support-faqs.md)。

Adobe Analytics for Audio and Video支援所有主要裝置，包括：

* iOS 和 Android 智慧型手機和平板電腦
* 適用於 ROKU、AppleTV、FireTV 以及 Android TV 的 OTT 裝置
* 適用於桌上型電腦和筆記型電腦的 JavaScript 瀏覽器

當新版裝置發行時，Media SDK會定期更新，而您可使用SDK與現今最大的媒體播放器整合，包括Brightcove和Ooyala。

對於目前沒有SDK支援的裝置或平台，或您不想使用SDK的情況，您可以實作Media Collection API。 Media Collection API可讓您直接從裝置或平台對Media Analytics後端進行REST風格的API呼叫。

下表列出目前支援的裝置和平台。 若要下載最新版 SDK，請參閱[下載 SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)。如果未列出裝置，請連絡您的客戶服務或解決方案顧問以取得該裝置的狀態。

| 串流平台與裝置 |  | 使用AEP SDK的Media Launch Extension | Media SDK | 媒體收集 API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| 網頁／行動網路 |  |  |  |  |
|  | JavaScript瀏覽器 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| 行動應用程式 |  |  |  |  |
|  | iOS 裝置 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android 裝置 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows裝置 |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV(tvOS) | 預計2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | 羅庫 |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>（原生） |
|  | Fire TV(Fire OS) | 預計2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | 預計2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | 遊戲主機（例如Xbox ONE、Sony PS3/PS4） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 機上盒（例如xfinity X1） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 智慧型電視（例如Samsung、LG、Sony、Vizio） |  | ![](/help/assets/icon-blue-check.png)   <br>（網路型）    | ![](/help/assets/icon-blue-check.png) |
| 其他 |  |  |  |  |
|  | 全新連接的裝置 |  |  | ![](/help/assets/icon-blue-check.png) |

1. 這些SDK的支援將於2021年8月31日截止。 如需詳細資訊，請 [參閱「媒體分析SDK終止支援常見問答」](/help/sdk-implement/end-of-support-faqs.md)。

如需每個SDK支援之最低平台版本的詳細資訊，請參閱最低平 [台版本支援](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)
