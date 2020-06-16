---
title: Media Analytics SDK 支援終止常見問題集
description: 此主題包含有關 Media Analytics SDK 支援終止的常見問題集。
translation-type: ht
source-git-commit: 38adc54438f85ca8ece8c77d9ff0d0aa14eb6605
workflow-type: ht
source-wordcount: '703'
ht-degree: 100%

---


# Media Analytics SDK 支援終止常見問題集

我們於 2021 年 8 月 31 日停止支援第 4 版 Mobile SDK 後，Adobe 也將停止支援 Media Analytics SDK iOS 版和 Android 版。2021 年 8 月 31 日後，Adobe 將不為 Media Analytics SDK 提供修正、作業系統相關更新或支援。提醒您，在移轉至這些新 Experience Platform SDK 的過程中，必須實作 [Media Analytics 擴充功能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)，才能啟用 Adobe Analytics for Audio and Video。

## 5 大須知事項

1. 2021 年 8 月 31 日後，我們將不再支援 Mobile v4 SDK。請改用 iOS 和 Android 專用的 Adobe Experience Platform (AEP) SDK。如需詳細資訊，請參閱[第 4 版行動 SDK 支援終止常見問題集](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)。

1. Analytics for Audio and Video 實作需要 AEP SDK，而且必須使用 Analytics 和 Media Analytics 擴充功能。自 2021 年 9 月 1 日起，您必須使用新的 AEP SDK 和擴充功能。請使用 Adobe Launch 來設定 Media Analytics 擴充功能。  如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch](https://docs.adobe.com/content/help/zh-Hant/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. 日後我們不會再開發 Media Analytics SDK iOS 版和 Android 版。從 2019 年秋季開始導入的新功能，會使用 Media Analytics 擴充功能和 Media Collection API 來啟用。

1. Analytics for Audio and Video 客戶仍可使用 Roku 和 Chromecast SDK。我們仍會將 Roku 和 Chromecast SDK 視為獨立式 SDK，並繼續提供增強和支援服務。  如果您使用 Media Analytics JS SDK，則可繼續使用該獨立式 SDK，或是使用 Adobe Launch 啟用 Media Analytics 擴充功能。

1. 在 2021 年 9 月 1 日前，Adobe 可能會自行決定針對高技術影響或商業曝光問題開發最新修正。Adobe 將根據客戶的意見判定影響和曝光程度，以及後續活動。

如有任何問題，請洽詢您的 Adobe 客戶成功案例經理。

## 常見問題解答

1. **Roku 和 Chromecast SDK 支援是否會受到影?**

   否。目前我們仍將 Roku 和 Chromecast SDK 視為獨立式 SDK，並繼續提供支援。&#x200B;
1. **此變更是否會影響 Media Analytics JS SDK 實作？**

   否。使用 Media Analytics JS SDK 的客戶可以繼續使用該 SDK，也可以透過 Adobe Launch 來予以啟用。
&#x200B;
1. **移轉至 Media Analytics 擴充功能的工作量為何？**

   工作量會因每個客戶的實作方式而異。  檢閱下列移轉文件後，如需其他支援，請洽詢諮詢和/或客戶服務。

   [Media Analytics 擴充功能：Android 移轉](https://docs.adobe.com/content/help/zh-Hant/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics 擴充功能：iOS 移轉](https://docs.adobe.com/content/help/zh-Hant/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics 擴充功能：新實作](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **我是否需要將 Launch 作為標記管理系統？如果我不想使用 Launch，該怎麼辦？**

   使用行動應用程式時，Launch 不會在網頁版中作為標記管理系統使用 (與網頁中的使用方式不同)。  在設定 SDK 擴充功能時，必須使用 Launch UI。這類似您使用 Adobe Mobile Services UI 來設定行動 v4 SDK 的方式。在安裝時，使用 Launch 的優點是可根據您選擇的擴充功能，為您提供自訂的安裝指示。

1. **此支援終止是否會影響 tvOS 的 SDK？**

   是。tvOS (10 以上版本) 的建議實作方法是移轉至 Media Analytics 擴充功能。  我們計畫於 2020 年 6 月推出 AEP SDK 支援和 Media Analytics 擴充功能支援。如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch - iOS](https://docs.adobe.com/content/help/zh-Hant/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)。

1. **此支援終止是否會影響 FireTV 和 AndroidTV 的 SDK&#x200B;？**

   是。FireTV 和 AndroidTV 的建議實作方法是移轉至 Media Analytics 擴充功能。我們計畫於 2020 年 6 月推出 AEP SDK 支援和 Media Analytics 擴充功能支援。如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch - Android](https://docs.adobe.com/content/help/zh-Hant/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)。
