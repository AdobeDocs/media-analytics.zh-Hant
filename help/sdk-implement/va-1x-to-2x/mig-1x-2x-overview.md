---
title: 移轉概述
description: 本主題概述從1.x版本移轉至2.x版本的Media SDK。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 移轉概述{#migration-overview}

透過新版簡化的 API (適用於初始化、設定和播放器委派)，從 VHL 1.x 移轉至 VHL 2.x 相當簡單明瞭。

以下為 1.x 和 2.x 的主要差異:

* **外掛程式、委派 -** 您不再需要為 Analytics、VideoPlayer 和 Heartbeat 執行外掛程式和委派。
* **設定 -** 您不再需要為 1.x 外掛程式實例化設定。

## 2.x的優點 {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* 您不再需要執行個體化Analytics、VideoPlayer和Heartbeat外掛程式的設定。 您只需使用和例項 `MediaHeartbeat` 實例化類 `MediaHeartbeatDelegate` 別 `MediaHeartbeatConfig` 即可。 這是初始化媒體分析所需的唯一實作。

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. 同時，請移除取得大量外掛程式作為輸入的 初始化的所有現有實施。您可以在下文中看到 1.x 和 2.x 實作的逐步比較: [程式碼比較: 1.x 和 2.x.](./code-comparison-1x-2x.md)

2.x 版的新 API 詳細說明: [API 1.x 版轉換至 2.x 版](./1x-2x-api-change.md)。
