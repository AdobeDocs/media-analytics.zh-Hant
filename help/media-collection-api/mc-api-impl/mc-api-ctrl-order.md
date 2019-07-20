---
seo-title: 控制事件順序
title: 控制事件順序
uuid: 007fcc6-be72-4b79-826d-588c957 cf15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# 控制事件順序{#controlling-the-order-of-events}

由於Media Collection API是REREFul，所以視訊追蹤是高度時間依賴性的操作，實施者可能會擔心到達後端的Media Collection API追蹤呼叫。後端&#x200B;*會*&#x200B;根據 `playerTime` 物件提供的時間戳記，將事件加入佇列及重新排序。然而，這項功能有其限制。目前，如果順序錯亂之呼叫間的延遲時間超過一秒，重新排序就可能會失敗。我們會在未來的更新中最佳化及/或設定「可接受的延遲時間」。
