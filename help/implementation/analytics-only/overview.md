---
title: 僅限Analytics的實施概觀
description: 適用於串流媒體的Adobe Analytics附加元件的先決條件和實作方法，用於僅限Analytics的實作。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 5%

---

# 僅限Analytics的實施概觀

僅限Analytics的實施使用Adobe Analytics for Streaming Media附加元件直接將資料傳送至Adobe Analytics，而不使用Edge Network。 這些方法仍受到完整支援。 若是新的實作，Adobe建議改用[Edge實作](/help/implementation/edge/overview.md)，因為這樣除Adobe Analytics外，還能讓Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP使用資料。

## 先決條件

1. **完成一般必要條件。** 請參閱[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認Adobe Analytics實作。** 僅限Analytics的串流媒體實作需要基本的Adobe Analytics實作。 請參閱[實作Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant)。

1. **取得媒體追蹤伺服器URL。** 請向您的Adobe Analytics代表詢問媒體追蹤伺服器URL (`collection-api-server` URL)。 網域通常遵循模式`[your_namespace].hb-api.omtrdc.net`。

1. **下載SDK或安裝擴充功能。** 根據您的平台，[下載目前的SDK](/help/getting-started/download-sdks.md)或安裝必要的標籤延伸模組。

## 選擇您的實作方法

每個頁面都涵蓋串流媒體特有的設定。 每個事件和每個變數的程式碼都存在於[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)中。

| 程式碼基底 | 程式碼內 | 使用標籤 |
|---|---|---|
| 網頁(JavaScript) | [JavaScript](javascript.md) | [Media Analytics標籤擴充功能](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| API | [媒體收集API](media-collection-api.md) | — |

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [實作總覽](/help/implementation/overview.md)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
