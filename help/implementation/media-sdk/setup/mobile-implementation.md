---
title: 如何使用串流媒體標籤來設定行動SDK
description: 了解如何為行動應用程式實作Adobe串流媒體。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 28%

---

# 安裝行動SDK {#install-mobile-sdks}

若要在Android或iOS上為行動應用程式實作串流媒體，請安裝並設定下列項目：

* **Adobe Experience Platform Mobile SDK**

   若要收集資料，請使用Adobe Experience Platform中的標籤。 Adobe Experience Platform 中的標記是標記管理解決方案，可讓您部署 Analytics 程式碼以及其他標記需求。 

* **Android適用的Media SDK** 或 **Media SDK for iOS**

* **Adobe Media Analytics for Audio and Video 擴充功能**

若要下載SDK和其他檔案資源，請參閱 [取得Media SDK、使用標籤的擴充功能，以及OTT SDK](/help/getting-started/download-sdks.md)

* **獲取有效的配置參數**

   在您設定分析帳戶後，即可從Adobe代表取得這些參數。

* **在您的媒體播放器中加入下列API**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。

   * *提供播放器資訊的API*  — 這包括目前播放的相關資訊，例如媒體名稱、播放點位置、廣告或章節。
