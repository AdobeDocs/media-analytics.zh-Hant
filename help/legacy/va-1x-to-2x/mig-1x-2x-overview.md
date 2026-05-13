---
title: 移轉概觀
description: 了解如何將 Media SDK 1.x 版本移轉至 2.x 版本。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 87%

---

# 舊版移轉概觀：VHL 1.x 至 VHL 2.x {#migration-overview}

透過新版簡化的 API (適用於初始化、設定和播放器委派)，從 VHL 1.x 移轉至 VHL 2.x 相當簡單明瞭。

以下為 1.x 和 2.x 的主要差異：

* **外掛程式、代理人 —**&#x200B;您不再需要實作Analytics、VideoPlayer和Heartbeat的外掛程式和代理人。
* **設定 —**&#x200B;您不再需要將1.x外掛程式的設定具現化。

## 2.x 版的優點 {#benefits-of-two-x}

* 所有公用方法皆已整合至 `MediaHeartbeat` 類別，讓開發人員更容易實作。
* 所有設定現已整合至 `MediaHeartbeatConfig` 類別。
* 不再需要為 Analytics、VideoPlayer 和 Heartbeat 外掛程式實例化設定。 您只需要使用 `MediaHeartbeatDelegate` 和 `MediaHeartbeatConfig` 例項實例化 `MediaHeartbeat` 類別。 這是唯一需要初始化 Media Analytics 的實作。

  透過初始化 `MediaHeartbeat`，您可以安全地刪除 Analytics 外掛程式、VideoPlayer 外掛程式和 Heartbeat 外掛程式的所有實作。 此外，請移除所有現有的初始化實作，這些實作會將插件陣列作為輸入參數。 您可以在下文中看到 1.x 和 2.x 實作的逐步比較：[程式碼比較：1.x 和 2.x.](./code-comparison-1x-2x.md)

2.x 版的新 API 詳細說明：[API 1.x 版轉換至 2.x 版](./1x-2x-api-change.md)。
