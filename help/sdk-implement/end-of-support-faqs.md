---
title: Media Analytics SDK支援終止常見問答集
description: 本主題包含有關Media Analytics SDK支援終止的常見問答集。
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# Media Analytics SDK支援終止常見問答集

在2021年8月31日終止對第4版行動SDK的支援後，Adobe也將終止對iOS和Android專用Media Analytics SDK的支援。 在2021年8月31日之後，Adobe將不提供Media Analytics SDK的修正、作業系統相關更新或支援。  在移轉至這些新的Experience Platform SDK的過程中，請記住，必須實作 [Media Analytics擴充功能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) ，才能啟用Adobe Analytics for Audio和Video。

## 5大須知事項

1. 2021年8月31日之後將不再支援行動v4 SDK。 您應移轉至iOS和Android專用的Adobe Experience Platform(AEP)SDK。

1. 「音訊和視訊分析」實作需要AEP SDK，並使用Analytics和Media Analytics擴充功能。 自2021年9月1日起，您應使用新的AEP SDK和擴充功能。  Media Analytics擴充功能是使用Adobe Launch來設定。  如需詳細資訊，請 [參閱從獨立媒體SDK移轉至Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. iOS和Android專用的Media Analytics SDK功能開發已結束。  從2019年秋季開始推出的新功能，會使用Media Analytics擴充功能和Media Collection API來啟用。

1. Roku和Chromecast SDK仍可供音訊和視訊分析客戶使用。 Roku和Chromecast SDK將繼續增強並支援為獨立SDK。  如果您使用適用於媒體分析的JS SDK，則可繼續使用獨立的SDK，或使用Adobe Launch啟用媒體分析擴充功能。

1. 在2021年9月1日之前，Adobe得自行決定針對高技術影響或業務曝光問題開發新修正。 根據客戶的意見，Adobe將決定影響和曝光程度，以及隨後的活動。

如有任何疑問，請洽詢您的Adobe客戶成功經理。

## 常見問題解答

1. **Roku和Chromecast SDK的支援是否會受到影&#x200B;響？**

   無.  目前，Roku和Chromecast SDK仍將支援為獨立SDK&#x200B;。
1. **此變更是否會影響Media Analytics JS SDK實作&#x200B;?**

   無.  使用JS SDK for Media Analytics的客戶可繼續使用SDK或透過Adobe Launch啟用SDK。
&#x200B;
1. **移轉至Media Analytics擴充功能的工作量為何&#x200B;?**

   LOE取決於每個客戶的實施，因此會有所不同。  在檢閱下列移轉檔案後，請洽詢諮詢和／或客戶服務以取得其他支援。

   [媒體分析擴充功能： Android移轉](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [媒體分析擴充功能： iOS移轉](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [媒體分析擴充功能： 新建](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **我是否需要將Launch作為標籤管理系統？ 如果我不想使用Launch，該怎麼辦？**

   對於行動裝置，Launch是必要項目，以設定媒體擴充功能，例如Mobile Services UI。 在行動應用程式使用案例中，它不會用作標籤管理系統。

1. **此支援終止是否會影響適用於tvOS的SDK?**

   是的，對於tvOS（10+版），建議實作是移轉至「媒體分析擴充功能」。  AEP SDK支援和Media Analytics Extension支援計畫於2020年6月推出。  如需詳細資訊，請 [參閱從獨立的Media SDK移轉至Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)。

1. **此項支援終止是否會影響FireTV和AndroidTV的SDK&#x200B;?**

   是的，對於FireTV和AndroidTV，建議實作是移轉至「媒體分析擴充功能」。  AEP SDK支援和Media Analytics Extension支援計畫於2020年6月推出。  如需詳細資訊，請 [參閱從獨立的Media SDK移轉至Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)。
