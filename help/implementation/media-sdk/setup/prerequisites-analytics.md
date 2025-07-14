---
title: 僅實作 Adob​​e Analytics 的先決條件
description: 瞭解搭配僅限串流媒體的Adobe Analytics實施使用串流媒體收集的先決條件
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 44%

---

# 僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件

本節中說明的必備條件專用於透過Adobe-Analytics實作(不使用Edge時)實作串流媒體收集。

1. **完成一般必要條件**<br>
無論您是實作僅限Adobe Analytics的實施或適用於Edge實施的串流媒體收集，請確保您符合[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認您有Adobe Analytics實作**<br>
若使用僅限Analytics的實作來實作串流媒體收集，則還需要Adobe Analytics基本實作。 請參閱[實作 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)以取得詳細資訊。

1. **取得媒體追蹤伺服器 URL**<br>
請向您的 Adobe Analytics 代表詢問媒體追蹤伺服器 URL。這是行動SDK、JavaScript SDK和Roku非集合API追蹤伺服器的`collection-api-server` URL。 API 實作的網域名稱是：`[your_namespace].hb-api.omtrdc.net`。

1. **下載目前的 Media SDK 或實作必要的擴充功能**<br>
根據實作路徑，針對 Web、行動或過頂平台[下載目前的 SDK](/help/getting-started/download-sdks.md)。必須實作必要的擴充功能才能啟用串流媒體收集擴充功能路徑。

1. **啟用 Adobe Analytics 報表**<br>
要在 Analytics 中啟用報表並檢視您正在收集的內容和廣告資料，您必須在 Analytics 中啟用報表。請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。
