---
title: 內容型別
description: 報告串流格式（VOD、即時、線性、播客、歌曲等）。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# 內容型別

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容型別**&#x200B;報告維度。 如需如何收集此變數，請參閱[內容型別](/help/implementation/variables/core/content-type.md)。*

>[!ENDSHADEBOX]

**內容型別**&#x200B;維度會報告資料流的格式（例如，視訊為VOD、直播或線性，音訊則為歌曲、播客或有聲書）。

## 如何填入此維度

內容型別由播放器在工作階段開始時設定，並在每個事件中執行。 並非衍生而來；所報告的值與收集期間所傳送的值相符。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.contentType`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>如果未設定內容型別或內容型別為空白，則維度會針對工作階段報告`missing_content_type`。 使用此值來尋找需要修正的實作。

## 維度項目

Adobe定義的值會填入內建區段和報表。 接受自訂字串，但不會比對內建區段。

| 資料流類型 | 建議值 |
| --- | --- |
| 影片 | `vod`, `live`, `linear`, `ugc`, `dvod` |
| 音訊 | `song`, `podcast`, `audiobook`, `radio` |

## 建議的區段

| 區段 | 規則 |
| --- | --- |
| [!UICONTROL VOD內容] | 內容型別= `vod` |
| [!UICONTROL 即時內容] | 內容型別= `live` |
| [!UICONTROL 線性內容] | 內容型別= `linear` |
