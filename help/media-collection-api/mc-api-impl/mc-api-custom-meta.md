---
title: 自訂中繼資料支援
description: 自訂中繼資料支援
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# 自訂中繼資料支援{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自訂索引鍵:值配對。這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON 索引鍵應包含索引鍵:值配對的物件。索引鍵只能包含英數字元、底線及點/句號。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
