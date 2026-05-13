---
title: 僅實作 Adob​​e Analytics 的先決條件
description: 瞭解將串流媒體收集用於僅限Adobe Analytics的實施或Edge實施的先決條件
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 16%

---

# Edge 實作的先決條件

本節中說明的先決條件專用於透過Edge實施實施Adobe串流媒體收集。

1. **完成一般必要條件**<br>
無論您是實作僅限Adobe Analytics的實施或適用於Edge實施的串流媒體收集，請確保您符合[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認您正在實作與Edge Network和串流媒體集合相容的Adobe解決方案**<br>
透過Edge實作串流媒體收集時，您還必須具備有效的Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer或Real-Time Customer Data Platform實作。 如需詳細資訊，請參閱下列檔案資源：
   * [Customer Journey Analytics指南](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hant)
   * [實施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer檔案](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant)
   * [Real-Time Customer Data Platform檔案](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **取得媒體追蹤伺服器URL**<br>
請向您的Customer Journey Analytics代表詢問媒體追蹤伺服器URL。<!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **使用Edge Network實作串流媒體收集**<br>
請依照[使用Edge Network實作串流媒體收集](/help/implementation/edge/implementation-edge.md)中的步驟操作。
