---
title: 內容
description: 報告每個播放的不重複媒體，並以內容ID作為索引鍵。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---


# 內容

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**內容**報告維度。 如需如何收集此變數，請參閱[內容識別碼](/help/implementation/variables/core/content-id.md)。*

>[!ENDSHADEBOX]

**Content**&#x200B;維度會報告每個播放的不重複媒體，並以工作階段開始時設定的內容ID作為索引鍵。 這是串流媒體報表的主要劃分，也是分類維度（例如視訊名稱、視訊長度、資產ID、首播日期和內容評分）的聯結索引鍵。

## 如何填入此維度

內容由播放器在工作階段開始時設定為資產的穩定識別碼。 工作階段的每個後續事件都會報告相同的內容ID。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.name`收集。 持續存在於造訪期間。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>內容ID為必要項。 如果未設定或空白，則工作階段會從串流媒體報表中刪除，且不會出現在任何媒體報表或[!UICONTROL 所有串流媒體]區段中。

## 維度項目

每個專案都是工作階段開始時回報的唯一內容ID。 使用穩定的識別碼(例如，內部CMS ID、產業ID （例如EIDR或TMS/Gracenote）或持續性概要)，以便相同資產的工作階段會隨著時間累加為單一條列專案。

## 建議的區段

| 區段 | 規則 |
| --- | --- |
| [!UICONTROL 所有串流媒體] | 內容(ID)已存在 |
