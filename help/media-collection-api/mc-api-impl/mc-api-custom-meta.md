---
title: 自訂中繼資料支援
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 自訂中繼資料支援{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自訂索引鍵:值配對。這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON 索引鍵應包含索引鍵:值配對的物件。索引鍵只能包含英數字元、底線及點/句號。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

