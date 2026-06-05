---
title: 瞭解Adobe串流媒體服務的先決條件
description: 開始使用串流媒體服務。 瞭解實作所需的專案。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# 先決條件 {#prerequisites}

開始實作Adobe串流媒體服務前，請先完成下列工作：

1. **確認您的定價模式**<br>
Customer Journey Analytics串流媒體收集附加元件和Adobe Analytics for Streaming Media附加元件目前的定價模型是以視訊串流為基礎。 如有必要，請聯絡您的銷售代表或Adobe客戶團隊，因為此附加元件是針對Adobe Analytics和Adobe Experience Platform分開銷售。

1. **啟用Adobe Analytics報表** *（僅限Analytics實施）*<br>
若要在Analytics中啟用報表並檢視您正在收集的內容和廣告資料，您必須啟用報表。 請參閱[為僅限Analytics的實施設定報告](/help/reporting/setup/analytics-reporting.md)。

1. **設定身分**<br>

   身分設定需求會因您的實作方法而異：

   * **Edge實作**：身分是透過Adobe Experience Platform身分識別名稱空間設定來處理。 不需要個別設定Identity Service。 如需詳細資訊，請參閱[Edge實作概觀](/help/implementation/edge/overview.md)。

   * **僅限Analytics的實作**：必須啟用Adobe Experience Platform Identity Service，才能在CX Enterprise解決方案中一致地識別訪客。 Identity Service會為每個網站訪客指派不重複的永久ID，並可讓該ID在您訂閱的所有CX Enterprise解決方案之間共用。

     如需詳細資訊，請參閱[Adobe Experience Platform Identity Service檔案](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)。

1. **檢視您的實作的其他先決條件**

   根據您計畫實作串流媒體服務的方式，檢視下列任一實作方法的先決條件：

   * [僅限Analytics的實施概觀](/help/implementation/analytics-only/overview.md)

   * [Edge實作概觀](/help/implementation/edge/overview.md)

   使用[實施概觀](/help/implementation/overview.md)以確定哪種實施方法適合您。
