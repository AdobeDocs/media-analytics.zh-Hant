---
title: 如何使用適用於串流媒體服務的標籤來設定行動SDK
description: 瞭解如何為行動應用程式實作Adobe串流媒體服務。
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 70%

---

# 安裝 Mobile SDK {#install-mobile-sdks}

若要在Android或iOS上實作適用於行動應用程式的Adobe串流媒體服務，請安裝和設定下列專案：

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
