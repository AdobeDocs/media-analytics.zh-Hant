---
title: 設定Media Analytics標籤擴充功能
description: 使用Adobe Media Analytics (3.x SDK) for Audio and Video標籤擴充功能來實作僅限Analytics的串流媒體。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%

---

# 設定Media Analytics標籤擴充功能

Adobe Media Analytics (3.x SDK) for Audio and Video標籤擴充功能會透過Tags部署Media SDK for JavaScript (3.x)，不需要手動安裝JavaScript。 本頁涵蓋標籤設定。 若要改為在程式碼中安裝SDK，請參閱[設定適用於串流媒體的JavaScript](javascript.md)。 若為新實作，請考慮建議的[Web SDK標籤延伸模組](/help/implementation/edge/web-sdk-tags.md) Edge路徑。

* **必要條件**：完成[僅限Analytics的實施概述](overview.md)。

## 安裝並設定擴充功能

在資料收集UI中安裝和設定擴充功能，以將媒體追蹤器例項新增至已啟用標籤的網站。 如需安裝和設定詳細資料，請參閱[Adobe Media Analytics (3.x SDK) for Audio and Video擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant)。

## 追蹤媒體事件

設定擴充功能後，可使用其追蹤器方法來追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Media SDK JS 3.x**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為僅限Analytics的實作](/help/reporting/setup/analytics-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [Adobe Media Analytics (3.x SDK) for Audio and Video擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hant)
>* [設定適用於串流媒體的JavaScript （程式碼）](javascript.md)
>* [事件總覽](/help/implementation/events/overview.md)
