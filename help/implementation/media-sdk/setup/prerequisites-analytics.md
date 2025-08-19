---
title: 僅實作 Adob​​e Analytics 的先決條件
description: 瞭解在僅限Adobe Analytics的實施中使用適用於串流媒體的Adobe Analytics附加元件的先決條件
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 43%

---

# 僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件

本節中說明的必備條件專用於為僅限Adobe Analytics的實作實作實作Adobe Analytics for Streaming Media附加元件(若不使用Edge)。

1. **完成一般必要條件**<br>
無論您是實作僅限Adobe Analytics的實作或Edge實作的串流媒體服務，請確定您符合[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認您有Adobe Analytics實作**<br>
針對僅Analytics實施作業來實施適用於串流媒體的Adobe Analytics附加元件時，還需要Adobe Analytics基本實施。 請參閱[實作 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)以取得詳細資訊。

1. **取得媒體追蹤伺服器 URL**<br>
請向您的 Adobe Analytics 代表詢問媒體追蹤伺服器 URL。這是行動SDK、JavaScript SDK和Roku非集合API追蹤伺服器的`collection-api-server` URL。 API 實作的網域名稱是：`[your_namespace].hb-api.omtrdc.net`。

1. **下載目前的 Media SDK 或實作必要的擴充功能**<br>
根據實作路徑，針對 Web、行動或過頂平台[下載目前的 SDK](/help/getting-started/download-sdks.md)。必須實作必要的擴充功能才能啟用適用於串流媒體的Adobe Analytics附加元件。

1. **啟用 Adobe Analytics 報表**<br>
要在 Analytics 中啟用報表並檢視您正在收集的內容和廣告資料，您必須在 Analytics 中啟用報表。請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。
