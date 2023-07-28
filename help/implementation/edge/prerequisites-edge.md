---
title: 僅限Adobe Analytics實作的先決條件
description: 瞭解將串流媒體用於僅限Adobe Analytics實施的先決條件
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Edge實作的先決條件

本節中說明的先決條件專用於透過Edge實施作業實施串流媒體。

1. **完成一般必要條件**<br>
無論您是針對Adobe Analytics實作還是Edge實作實作實作來實作串流媒體，請確保您符合 [一般必要條件](/help/getting-started/prereqs.md).

1. **確認您正在實作與Edge和串流媒體相容的Adobe解決方案**<br>
使用Edge實作串流媒體時，您還必須具備有效的Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer或Real-time Customer Data Platform實作。 如需詳細資訊，請參閱下列檔案資源：
   * [Customer Journey Analytics 指南](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hant)
   * [實施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant)
   * [Adobe Journey Optimizer檔案](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant)
   * [Real-time Customer Data Platform檔案](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **取得媒體追蹤伺服器URL**<br>
請向您的Customer Journey Analytics代表詢問媒體追蹤伺服器URL。 <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **安裝Media Analytics與Edge**<br>
請依照中的步驟操作 [安裝Media Analytics與Experience Platform Edge](/help/implementation/edge/implementation-edge.md).