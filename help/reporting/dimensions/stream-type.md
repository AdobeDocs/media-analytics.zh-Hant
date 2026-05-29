---
title: 資料流類型
description: 擷取每個媒體工作階段是否為音訊或視訊內容。
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%

---


# 資料流類型

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**資料流型別**報告維度。 如需如何收集此變數，請參閱[資料流型別](/help/implementation/variables/core/stream-type.md)。*

>[!ENDSHADEBOX]

**資料流型別**&#x200B;維度會擷取每個媒體工作階段是否為音訊或視訊內容。 為報表套裝啟用[媒體核心](/help/implementation/media-sdk/setup/media-reports-enable.md)後，它就會在Adobe Analytics中使用，若有任何資料集包含串流媒體資料，也能在Customer Journey Analytics中使用。

## 如何填入此維度

串流型別由播放器在工作階段開始時設定，並持續進行工作階段關閉呼叫。 它不是計算或衍生的。 報告的值與收集期間傳送的值完全相符。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.streamType`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>如果未設定資料流型別，則會針對該工作階段取消填入維度。 這些工作階段會從內建的「僅限音訊」和「僅限視訊」區段中排除，如果搭配資料流型別劃分使用，「所有串流媒體」區段會計算不足。

## 維度項目

| 值 | 說明 |
| --- | --- |
| `video` | 工作階段是影片內容。 |
| `audio` | 會議是播客、有聲書或音樂串流等音訊內容。 |

技術上來說，集合API接受自訂值，但並不建議使用。 這些區段不符合下列所述的內建區段，並可能導致跨實施的報告不一致。

## 建議的區段

資料流型別是Adobe Analytics內建[!UICONTROL 媒體資料流型別]區段的基礎。 使用這些區段，將任何串流媒體報表的範圍限定為特定內容型別：

| 區段 | 規則 |
| --- | --- |
| [!UICONTROL 所有串流媒體] | 內容(ID)已存在 |
| [!UICONTROL 僅限音訊] | 內容(ID)存在且資料流型別= `audio` |
| [!UICONTROL 僅限視訊] | 內容(ID)存在且資料流型別!=`audio` |

>[!TIP]
>
>[!UICONTROL 僅視訊]區段使用`!=`規則而非`= video`來正確擷取工作階段，其中資料流型別可能已設定為不是`audio`的自訂值。
