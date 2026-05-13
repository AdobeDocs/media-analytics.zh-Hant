---
title: 傳送 QoE 資料
description: 了解如何使用 qoeData JSON 索引鍵傳送事件。
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gLf-vtHwf0I5JVPyfUj2479exPaAXYu2gyYUU2V5Glw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 55
ht-degree: 100%

---

# 傳送 QoE 資料{#sending-qoe-data}

您可以使用稱為 `qoeData` 的額外 JSON 索引鍵為每個事件裝飾，將其放置於 JSON 要求內文中的 `params` 索引鍵旁。

>[!NOTE]
>
>請務必參閱 [JSON 驗證結構](mc-api-validate-reqs.md)以確認參數類型，以及瞭解參數為強制或選用性質。
