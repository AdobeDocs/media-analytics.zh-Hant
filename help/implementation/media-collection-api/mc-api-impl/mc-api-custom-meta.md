---
title: 自訂中繼資料支援
description: 瞭解如何在sessionStart、chapterStart和adStart事件中提供自訂索引鍵：值配對。
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 62%

---

# 自訂中繼資料支援{#custom-metadata-support}

您可以在:value、`sessionStart`和`chapterStart`事件中提供自訂索引鍵`adStart`配對。 這些資訊必須以 JSON 索引鍵 `customMetadata` 提供，並放置在 `params` 索引鍵旁。

`customMetadata` JSON索引鍵應包含索引鍵:value配對的物件。 索引鍵只能包含英數字元、底線及點/句號。

[MA Collection API 事件](../mc-api-ref/mc-api-events-req.md)

## 範例

目前您可以使用下列索引鍵`sessionStart`配對來傳送:value事件：

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
