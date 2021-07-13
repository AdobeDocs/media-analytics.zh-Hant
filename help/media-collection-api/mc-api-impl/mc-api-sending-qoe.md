---
title: 傳送 QoE 資料
description: 了解如何使用qoeData JSON索引鍵傳送事件。
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# 傳送 QoE 資料{#sending-qoe-data}

您可以使用稱為 `qoeData` 的額外 JSON 索引鍵為每個事件裝飾，將其放置於 JSON 要求內文中的 `params` 索引鍵旁。

>[!NOTE]
>
>請務必參閱 [JSON 驗證結構](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)以確認參數類型，以及瞭解參數為強制或選用性質。
