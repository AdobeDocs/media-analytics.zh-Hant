---
title: 控制事件順序
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 控制事件順序{#controlling-the-order-of-events}

由於媒體收集 API 是 RESTful API，而且視訊追蹤是高度依賴時間的作業，實作者可能會擔心媒體收集 API 追蹤呼叫未依照順序抵達後端。後端&#x200B;*會*&#x200B;根據 `playerTime` 物件提供的時間戳記，將事件加入佇列及重新排序。然而，這項功能有其限制。目前，如果順序錯亂之呼叫間的延遲時間超過一秒，重新排序就可能會失敗。我們會在未來的更新中最佳化及/或設定「可接受的延遲時間」。
