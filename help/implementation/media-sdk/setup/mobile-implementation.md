---
title: 如何使用標記為串流媒體設定 Mobile SDK
description: 了解如何為行動應用程式實作 Adobe Streaming Media。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 81%

---

# 安裝 Mobile SDK {#install-mobile-sdks}

若要在Android或iOS上實作適用於行動應用程式的串流媒體收集附加元件，請安裝和設定下列專案：

* **Adobe Experience Platform Mobile SDK**

  若要收集資料，請使用下列其中一項：
   * Adobe Experience Platform中的標籤。 Adobe Experience Platform 中的標記是標記管理解決方案，可讓您部署 Analytics 程式碼以及其他標記需求。
   * Adobe Experience Platform Edge

* **Android 適用的 Media SDK** 或 **iOS 適用的 Media SDK**

* **Adobe Media Analytics for Audio and Video 擴充功能**

若要下載 SDK 和需要其他文件資源，請參閱[取得 Media SDK、使用標記的擴充功能和 OTT SDK](/help/getting-started/download-sdks.md)

* **取得有效設定參數**

  設定 Analytics 帳戶之後，可以向 Adobe 代表取得這些參數。

* **在您的媒體播放器中包含以下 API**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。

   * *提供播放器資訊的 API* - 此包含目前播放的資訊，例如媒體名稱、播放點位置、廣告或章節。
