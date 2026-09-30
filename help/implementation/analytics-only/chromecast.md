---
title: 設定適用於串流媒體的Chromecast
description: 安裝並設定適用於Chromecast且僅限Analytics串流媒體實作的Media SDK 。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%
---
# 設定適用於串流媒體的Chromecast

Chromecast適用的Media SDK會直接從Chromecast接收器應用程式將串流媒體資料傳送到Adobe Analytics。 SDK及其檔案託管在GitHub上。

* **必要條件**：
  * 完成[僅限Analytics的實作概觀](overview.md)。
  * [下載Chromecast適用的Media SDK](/help/getting-started/download-sdks.md)。

## 安裝和設定SDK

將SDK新增到您的Chromecast接收器應用程式，並依照規範參考中所述設定追蹤器：

* [設定Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Chromecast SDK API參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## 追蹤媒體事件

建立追蹤器後，請使用其追蹤器方法來追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Chromecast**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [Chromecast SDK API參考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
