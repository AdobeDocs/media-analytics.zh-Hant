---
title: 控制事件順序
description: 控制事件順序
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# 控制事件順序{#controlling-the-order-of-events}

由於媒體收集 API 是 RESTful API，而且視訊追蹤是高度依賴時間的作業，實作者可能會擔心媒體收集 API 追蹤呼叫未依照順序抵達後端。後端&#x200B;*會*&#x200B;根據 `playerTime` 物件提供的時間戳記，將事件加入佇列及重新排序。然而，這項功能有其限制。目前，如果順序錯亂之呼叫間的延遲時間超過一秒，重新排序就可能會失敗。我們會在未來的更新中最佳化及/或設定「可接受的延遲時間」。
