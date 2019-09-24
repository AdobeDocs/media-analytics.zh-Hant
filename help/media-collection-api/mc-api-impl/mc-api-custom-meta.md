---
seo-title: 自訂中繼資料支援
title: 自訂中繼資料支援
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 自訂中繼資料支援{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. 這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON金鑰應包含key:value配對的物件。 索引鍵只能包含英數字元、底線及點/句號。

[MA Collection API事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

