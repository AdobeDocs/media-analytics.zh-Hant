---
title: 移轉總覽
description: 了解如何從Media SDK 1.x版移轉至2.x版。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 79%

---

# VHL 1.x至VHL 2.x的舊版移轉概觀 {#migration-overview}

從VHL 1.x移轉至VHL 2.x的程式相當簡單明瞭，新版本提供簡化的API，以用於初始化、設定和播放器委派。i

以下為 1.x 和 2.x 的主要差異:

* **外掛程式、委派 -** 您不再需要為 Analytics、VideoPlayer 和 Heartbeat 執行外掛程式和委派。
* **設定 -** 您不再需要為 1.x 外掛程式實例化設定。

## 2.x 版的優點 {#benefits-of-two-x}

* 所有公用方法皆已整合至 `MediaHeartbeat` 類別，讓開發人員更容易實作。
* 所有設定現已整合至 `MediaHeartbeatConfig` 類別。
* 不再需要為 Analytics、VideoPlayer 和 Heartbeat 外掛程式實例化設定。您只需要使用 `MediaHeartbeatDelegate` 和 `MediaHeartbeatConfig` 例項實例化 `MediaHeartbeat` 類別。這是唯一需要初始化 Media Analytics 的實施。

   透過初始化 `MediaHeartbeat`，您可以安全地刪除 Analytics 外掛程式、VideoPlayer 外掛程式和 Heartbeat 外掛程式的所有實作。同時，請移除取得大量外掛程式作為輸入的 初始化的所有現有實施。您可以在下文中看到 1.x 和 2.x 實作的逐步比較: [程式碼比較: 1.x 和 2.x.](./code-comparison-1x-2x.md)

2.x 版的新 API 詳細說明: [API 1.x 版轉換至 2.x 版](./1x-2x-api-change.md)。
