---
title: 了解 Media Analytics SDK 終止支援常見問答
description: 此主題包含有關 Media Analytics SDK 終止支援的常見問題集。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b955b20495a504020a214c3a9e32b676701ee4cc
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 79%

---

# Media Analytics Mobile SDK 終止支援常見問題集

我們於2021年8月31日停止支援第4版Mobile SDK，屆時Adobe也將停止支援iOS和Android適用的Media Analytics Mobile SDK。 (其中不包括仍支援的適用於網頁(JS)和OTT平台（例如Chromecast和Roku）的Media Analytics SDK。)

這表示Adobe不再提供Media Analytics Mobile SDK的修正、作業系統相關更新或支援。 移轉至新Experience PlatformSDK時，請注意 [Media Analytics擴充功能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) 必須實作才能啟用適用於串流媒體的 Adobe Analytics。


## 5 大須知事項

1. 自2021年8月31日起，不再支援Mobile v4 SDK。 請移轉至 iOS 和 Android 專用的 Adobe Experience Platform (AEP) Mobile SDK。如需詳細資訊，請參閱[第 4 版 Mobile SDK 支援終止常見問答](https://developer.adobe.com/client-sdks/documentation/v4-end-of-life-faq/)。

1. 適用於串流媒體的 Analytics 實作需要 AEP Mobile SDK，而且必須使用 Analytics 和 Media Analytics 擴充功能。自2021年9月1日起，您應使用新的AEP Mobile SDK和擴充功能。  請使用 Adobe 標記來設定 Media Analytics 擴充功能 (資料收集)。如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. 日後我們不會再開發 Media Analytics SDK iOS 版和 Android 版。從 2019 年秋季開始導入的新功能，會使用 Media Analytics 擴充功能和 Media Collection API 來啟用。

1. 適用於串流媒體的 Analytics 客戶仍可使用 Roku 和 Chromecast SDK。我們仍會將 Roku 和 Chromecast SDK 視為獨立式 SDK，並繼續提供增強和支援服務。如果您使用 Media Analytics JS SDK，則可繼續使用該獨立式 SDK，或是使用 Adobe Data Collection (舊稱 Adobe Launch) 啟用 Media Analytics 擴充功能。

如有任何問題，請洽詢您的Adobe帳戶團隊。

## 常見問題解答

1. **Roku 和 Chromecast SDK 支援是否會受到影響？**

   否。目前我們仍將 Roku 和 Chromecast SDK 視為獨立式 SDK，並繼續提供支援。&#x200B;
1. **此變更是否會影響 Media Analytics JS SDK 實作？**

   否。使用 Media Analytics JS SDK 的客戶可以繼續使用該 SDK，也可以透過 Adobe Launch 來予以啟用。
&#x200B;
1. **移轉至 Media Analytics 擴充功能的工作量為何？**

   工作量會因每個客戶的實作方式而異。檢閱下列移轉文件後，如需其他支援，請洽詢諮詢和/或客戶服務。

[Media Analytics 擴充功能：Android 移轉](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics 擴充功能：iOS 移轉](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics 擴充功能：新實作](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **我是否需要將 Launch 作為標記管理系統？如果我不想使用 Launch，該怎麼辦？**

   使用行動應用程式時，Launch 不會在網頁版中作為標記管理系統使用 (與網頁中的使用方式不同)。在設定 SDK 擴充功能時，必須使用 Launch UI。這類似您使用 Adobe Mobile Services UI 來設定行動 v4 SDK 的方式。在安裝時，使用 Launch 的優點是可根據您選擇的擴充功能，為您提供自訂的安裝指示。

1. **此支援終止是否會影響 tvOS 的 SDK？**

   是。tvOS (10 以上版本) 的建議實作方法是移轉至 Media Analytics 擴充功能。如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)。

1. **此終止支援是否會影響 Fire TV 和 AndroidTV 的 SDK&#x200B;？**

   是。Fire TV 和 AndroidTV 的建議實作方法是移轉至 Media Analytics 擴充功能。如需詳細資訊，請參閱[從獨立式 Media SDK 移轉至 Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)。
