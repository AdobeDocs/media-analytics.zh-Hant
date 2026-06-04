---
title: 自訂中繼資料支援
description: 瞭解如何在sessionStart、chapterStart和adStart事件中提供自訂索引鍵：值配對。
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# 自訂中繼資料支援{#custom-metadata-support}

Media Collection API可讓您在`sessionStart`、`adStart`和`chapterStart`事件中，連同標準引數一起傳送自訂索引鍵/值組。 自訂中繼資料會透過個別媒體關閉事件轉送至&#x200B;**Adobe Analytics**。

若要讓此資料可在Analysis Workspace中使用，客戶必須定義自訂eVar並設定處理規則，以根據其使用案例填入這些資料。 對應到eVar或prop後，只要已設定[Analytics來源聯結器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)，資料也可透過對應的eVar路徑在Adobe Experience Platform中使用。

如需使用Experience Edge的XDM型實作，請參閱[自訂中繼資料支援 — XDM格式](/help/implementation/edge/custom-metadata.md)。

## 概觀

自訂中繼資料會作為`customMetadata`物件包含在要求內文中，並放置在`params`索引鍵旁。 它適用於三種事件型別：

| 事件 | 中繼資料套用至 |
|-------|-------------------|
| `sessionStart` | 主要內容（整個工作階段） |
| `adStart` | 個人廣告 |
| `chapterStart` | 內容章節或區段 |

## 結構

自訂中繼資料是事件層級的平面&#x200B;**物件** （機碼值組），以及`params`機碼：

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### 依事件型別區分的強制引數

| 事件 | 必要`params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### 金鑰命名需求

* 避免在自訂中繼資料索引鍵中使用`media.`首碼 — 這會對應至標準媒體欄位，並可能在Analytics報表中覆寫這些欄位
* `a.`首碼已保留給Adobe標準中繼資料，且不得使用

## 主要內容自訂中繼資料

與`sessionStart`一同傳送。 套用至要追蹤的主要媒體，並在整個廣告和章節呼叫中保持可用。 此處定義的任何自訂中繼資料都會由媒體後端在相應的關閉呼叫上自動合併。 它將與為廣告和章節定義的任何特定自訂中繼資料一起包含。

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## 廣告自訂中繼資料

與`adStart`一同傳送。 特定於每個個別廣告。 來自`sessionStart`的自訂中繼資料也會由廣告關閉呼叫上的媒體後端自動合併，連同此處定義的任何廣告特定自訂中繼資料。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## 章節自訂中繼資料

與`chapterStart`一同傳送。 特定於每個內容章節或區段。 來自`sessionStart`的自訂中繼資料也會由章節關閉呼叫上的媒體後端自動合併，連同此處定義的任何章節特定自訂中繼資料。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## 行為

* 所有自訂中繼資料值都必須是&#x200B;**字串**。 在傳送之前轉換數字和布林值。
* 自訂中繼資料出現在Analytics中，其前置詞為`c.` （例如`contentCategory` → `c.contentCategory`）
* 透過Analytics處理規則將自訂中繼資料對應至eVar、prop或內容資料變數
* `sessionStart`中繼資料會在整個工作階段中持續存在；更新需要新的工作階段
* 每個`adStart`和`chapterStart`事件都可以包含不同的自訂中繼資料

## 相關檔案

* [自訂中繼資料支援 — XDM格式](/help/implementation/edge/custom-metadata.md) — 透過Experience Edge傳送自訂中繼資料給Analytics和AEP
* [報告套裝資料的Adobe Analytics來源聯結器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics) — 將Analytics資料帶入Adobe Experience Platform

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->
