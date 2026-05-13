---
title: 僅實作 Adob​​e Analytics 的先決條件
description: 瞭解在僅限Adobe Analytics的實施中使用適用於串流媒體的Adobe Analytics附加元件的先決條件
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
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
source-wordcount: 243
ht-degree: 14%

---

# 僅實作 Adob&#x200B;&#x200B;e Analytics 的先決條件

本節中說明的必備條件專用於為僅限Adobe Analytics的實作實作實作Adobe Analytics for Streaming Media附加元件（若不使用Edge）。

1. **完成一般必要條件**<br>
無論您是實作僅限Adobe Analytics的實作或Edge實作的串流媒體服務，請確定您符合[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認您有Adobe Analytics實作**<br>
針對僅Analytics實施作業來實施適用於串流媒體的Adobe Analytics附加元件時，還需要Adobe Analytics基本實施。 請參閱[實作 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)以取得詳細資訊。

1. **取得媒體追蹤伺服器URL**<br>
請向您的Adobe Analytics代表詢問媒體追蹤伺服器URL。 這是行動SDK、JavaScript SDK和Roku非集合API追蹤伺服器的`collection-api-server` URL。 API 實作的網域名稱是：`[your_namespace].hb-api.omtrdc.net`。

1. **下載目前的Media SDK或實作必要的擴充功能**<br>
根據實作路徑，針對Web、行動或過頂平台[下載目前的SDK](/help/getting-started/download-sdks.md)。 必須實作必要的擴充功能才能啟用適用於串流媒體的Adobe Analytics附加元件。

1. **啟用Adobe Analytics報表**<br>
若要在Analytics中啟用報表並檢視您正在收集的內容和廣告資料，您必須在Analytics中啟用報表。 請參閱[啟用 Media 報表](/help/reporting/media-reports-enable.md)。
