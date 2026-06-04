---
title: 設定適用於串流媒體的Media Collection API
description: 使用Media Collection API透過RESTful HTTP呼叫直接傳送串流媒體資料給Adobe Analytics。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# 設定適用於串流媒體的Media Collection API

媒體收集API會使用RESTful HTTP呼叫，直接將串流媒體資料傳送至Adobe Analytics。 由於可完全自訂，因此可支援SDK未涵蓋的自訂追蹤和裝置。 當SDK不是您平台的選項時，請使用它。

* **必要條件**：完成[僅限Analytics的實施概述](overview.md)。

## 實作API

開啟含`sessionStart`要求的工作階段，然後將後續事件傳送至其傳回的工作階段。 如需完整的請求/回應格式、引數、驗證結構描述及實作指引，請參閱[媒體收集API參考](../media-collection-api/mc-api-overview.md)。

## 追蹤媒體事件

檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**媒體收集API**&#x200B;標籤，以取得確切的裝載。

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [媒體收集API參考](../media-collection-api/mc-api-overview.md)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
