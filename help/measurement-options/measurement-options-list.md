---
title: 測量選項
description: null
uuid: null
translation-type: ht
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: ht
source-wordcount: '293'
ht-degree: 100%

---


# 測量選項{#measurement-options}

您可以使用 Adobe Launch 搭配 Adobe Media Analytics 擴充功能、Media SDK 或 Media Collection API 來啟用音訊和視訊追蹤。

## Adobe Launch 搭配 Adobe Media Analytics 擴充功能

Adobe Launch 是新一代 Adobe 標籤管理解決方案。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。若要建立及維持您與 Launch 的整合，請使用擴充功能。擴充功能是指能擴充 Launch 使用者介面和用戶端功能的 JavaScript、HTML 及 CSS 套件。如需詳細資訊，請參閱 [Experience Platform Launch 使用手冊](https://docs.adobe.com/content/help/zh-Hant/launch/using/overview.html)

Adobe Media Analytics (MA) 擴充功能新增了音訊和視訊的核心 JavaScript Media SDK (Media 2.x SDK)。此擴充功能提供將 `MediaHeartbeat` 追蹤器例項新增至 Launch 網站或專案的功能。

Adobe Launch 搭配 Media Analytics 擴充功能使用前，請先符合以下條件：
* 您必須是 Adobe Experience Cloud 客戶。
* 您必須在網頁上部署 Launch 或 DTM 內嵌程式碼。
* [Analytics 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK 已整合一般最常使用的媒體播放器。

## Media Collection API (RESTful API)

與不支援 SDK 的播放器整合，或是不需要 SDK 整合時。<br>從 2.2.0 版開始，Video Heartbeat Library (VHL) SDK 已重新命名為 Media Analytics SDK，以支援音訊和視訊追蹤。Media 2.2.0 SDK 可完全回溯相容於 VHL 2.x SDK 系列。名稱變更只是命名慣例的變動，不代表功能有所改變。
