---
title: 僅實作 Adob​​e Analytics 的先決條件
description: 瞭解搭配僅Adobe Analytics實施使用串流媒體收集附加元件的先決條件
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# 僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件

本節中說明的必備條件專用於透過僅AdobeAnalytics實作(不使用Edge時)實作串流媒體收集附加元件。

1. **完成一般必要條件**<br>
無論您是實作僅限Adobe Analytics的實施或適用於Edge實施的串流媒體收集附加元件，請確保您符合 [一般必要條件](/help/getting-started/prereqs.md).

1. **確認您有Adobe Analytics實作**<br>
使用僅限Analytics的實施來實施串流媒體收集附加元件時，還需要Adobe Analytics基本實施。 請參閱[實作 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant)以取得詳細資訊。

1. **取得媒體追蹤伺服器 URL**<br>
請向您的 Adobe Analytics 代表詢問媒體追蹤伺服器 URL。這是 `collection-api-server` URL，適用於Mobile SDK、JavaScript SDK和Roku的非Collection API追蹤伺服器。 API 實作的網域名稱是：`[your_namespace].hb-api.omtrdc.net`。

1. **下載目前的 Media SDK 或實作必要的擴充功能**<br>
根據實作路徑，針對 Web、行動或過頂平台[下載目前的 SDK](/help/getting-started/download-sdks.md)。必須實作必要的擴充功能才能啟用串流媒體收集附加元件擴充功能路徑。

1. **啟用 Adobe Analytics 報表**<br>
要在 Analytics 中啟用報表並檢視您正在收集的內容和廣告資料，您必須在 Analytics 中啟用報表。請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。
