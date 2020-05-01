---
title: 測量選項
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# 測量選項

您可以使用Adobe Launch搭配Adobe Media Analytics擴充功能、Media SDK或Media Collection API來啟用音訊和視訊追蹤。

## Adobe Launch搭配Adobe Media Analytics擴充功能

Adobe Launch是Adobe的新一代標籤管理解決方案。 Launch提供簡單的方式，來部署和管理所有必要的分析、行銷和廣告標籤，以推動相關的客戶體驗。 若要建立並維護您與Launch的整合，請使用擴充功能。 副檔名是JavaScript、HTML和CSS套件，可擴充Launch UI和用戶端功能。 如需詳細資訊，請參閱 [Experience Platform Launch使用指南](https://docs.adobe.com/content/help/zh-Hant/launch/using/overview.html)

Adobe Media Analytics(MA)擴充功能新增了音訊和視訊的核心JavaScript Media SDK(Media 2.x SDK)。 此擴充功能提供將 `MediaHeartbeat` 追蹤器例項新增至 Launch 網站或專案的功能。

Adobe Launch搭配Media Analytics擴充功能需要：
* 您必須是Adobe Experience Cloud客戶。
* 您必須在網頁上部署Launch或DTM內嵌代碼。
* [Analytics 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK與最常用的媒體播放器整合。

## Media Collection API(RESTful API)

不需SDK支援或不需SDK整合時，就可與播放器整合。<br>從v2.2.0版開始，視訊心率程式庫(VHL)SDK會重新命名為Media Analytics SDK，以支援音訊和視訊追蹤。 Media 2.2.0 SDK完全向後相容於VHL 2.x SDK系列。 名稱變更只是命名慣例的變更，不代表功能變更。
