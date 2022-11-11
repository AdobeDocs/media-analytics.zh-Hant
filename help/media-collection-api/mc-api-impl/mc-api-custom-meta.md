---
title: 自訂中繼資料支援
description: "了解如何在sessionStart、chapterStart和adStart事件上提供自訂索引鍵：值配對。"
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 47%

---

# 自訂中繼資料支援{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自訂索引鍵:值配對。這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON 索引鍵應包含索引鍵:值配對的物件。索引鍵只能包含英數字元、底線及點/句號。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## 範例

目前，您可以傳送 `sessionStart` 事件，具有下列索引鍵：值組：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

針對上述設定，傳送至analytics的報表資料如下：

`c.a.media.channel=channel-2`

### 建議

建議您為自訂中繼資料使用個別的命名空間。 例如：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

在建議的範例中，傳送至分析的自訂中繼資料的報表資料如下：

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
