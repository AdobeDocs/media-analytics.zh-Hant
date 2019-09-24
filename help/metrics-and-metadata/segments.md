---
seo-title: 區段
title: 區段
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# 區段{#segments}

>[!NOTE]
>
>These reporting segments associated with Media Stream Type were introduced on 9/13/18 along with the `streamType` parameter.

| 區段 | 說明 | 規則 |
|---|---|---|
| 媒體資料流類型: 全部 | 對所有&#x200B;*媒體*&#x200B;串流資料劃分區段 | 「Content (ID) exists」 |
| 媒體資料流類型: 音效 | 對所有&#x200B;*音效*&#x200B;串流資料劃分區段 | 「Content (ID) exists」和「Media Stream Type = `audio`」 |
| 媒體資料流類型: 視訊 | 對所有&#x200B;*視訊*&#x200B;串流資料劃分區段 | 「Content (ID) exists」和「Media Stream Type ! = `audio`" |
| 媒體內容類型: VoD | 對所有 VoD 內容劃分區段 | "內容類型 = `vod`" |
| 媒體內容類型: 直播 | 對所有直播內容劃分區段 | "內容類型 = `live`" |
| 媒體內容類型: 線性播出 | 對所有線性播出內容劃分區段 | "內容類型 = `linear`" |
| 媒體內容類型: 播客 | 對所有播客內容劃分區段 | "內容類型 = `podcast`" |
| 媒體內容類型: 有聲書 | 對所有有聲書內容劃分區段 | "內容類型 = `audiobook`" |
| 媒體內容類型: AoD | 對所有 AoD 內容劃分區段 | "內容類型 = `aod`" |

