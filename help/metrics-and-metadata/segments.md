---
title: 媒體串流區段說明
description: 「了解與媒體資料流類型相關聯的報表區段，包括媒體資料流類型的區段、說明和規則。」
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics，細分"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 2d9d4352b0fd71710a9952ba4a77f6796ea9f5cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 66%

---

# 區段{#segments}

區段可讓您根據特性或網站互動來識別訪客的子集。串流媒體區段可讓您識別訪客資料流類型，例如音訊、即時或播客資料流。 如需Adobe Analytics區段的相關資訊，請參閱Adobe Analytics元件指南中的[關於區段和容器](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en)。

>[!NOTE]
>
>我們在 2018 年 9 月 13 日，推出了這些與媒體資料流類型相關的報表區段及 `streamType` 參數。

| 區段 | 說明 | 規則 |
|---|---|---|
| 媒體資料流類型: 全部 | 對所有&#x200B;*媒體*&#x200B;資料流劃分區段 | 「Content (ID) exists」 |
| 媒體資料流類型: 音訊 | 對所有&#x200B;*音效*&#x200B;資料流劃分區段 | 「Content (ID) exists」和「Media Stream Type = `audio`」 |
| 媒體資料流類型: 影片 | 對所有&#x200B;*視訊*&#x200B;資料流劃分區段 | 「Content (ID) exists」和「Media Stream Type != `audio`」 |
| 媒體內容類型: VoD | 對所有 VoD 內容劃分區段 | &quot;內容類型 = `vod`&quot; |
| 媒體內容類型: 直播 | 對所有直播內容劃分區段 | &quot;內容類型 = `live`&quot; |
| 媒體內容類型: 線性播出 | 對所有線性播出內容劃分區段 | &quot;內容類型 = `linear`&quot; |
| 媒體內容類型: 播客 | 對所有播客內容劃分區段 | &quot;內容類型 = `podcast`&quot; |
| 媒體內容類型: 有聲書 | 對所有有聲書內容劃分區段 | &quot;內容類型 = `audiobook`&quot; |
| 媒體內容類型: AoD | 對所有 AoD 內容劃分區段 | &quot;內容類型 = `aod`&quot; |
