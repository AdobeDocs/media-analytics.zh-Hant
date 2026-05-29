---
title: 如何使用適用於串流媒體服務的標籤來設定行動SDK
description: 瞭解如何為行動應用程式實作Adobe串流媒體服務。
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 220
ht-degree: 63%

---

# 安裝 Mobile SDK {#install-mobile-sdks}

>[!IMPORTANT]
>
>本頁涵蓋僅限Analytics的行動SDK實作。 如需建議的實作，請參閱[使用Edge Network實作串流媒體](/help/implementation/edge/edge-mobile-sdk.md)。

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
