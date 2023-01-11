---
title: 自訂中繼資料支援
description: 「了解如何在 sessionStart、chapterStart 和 adStart 事件中提供自訂索引鍵：值配對。」
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '127'
ht-degree: 100%

---

# 自訂中繼資料支援{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自訂索引鍵：值配對。這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON 索引鍵應包含索引鍵：值配對的物件。索引鍵只能包含英數字元、底線及點/句號。

[MA Collection API 事件](../mc-api-ref/mc-api-events-req.md)

## 範例

目前，您可以使用以下索引鍵：值配對來傳送 `sessionStart` 事件：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

對於上述設定，傳送到分析的報告資料如下：

`c.a.media.channel=channel-2`

### 建議

我們建議您為自訂中繼資料使用單獨的命名空間。例如：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

在建議的範例中，傳送至分析之自訂中繼資料的報告資料如下：

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
