---
title: 廣告載入
description: 報告用於每個串流媒體工作階段的廣告載入型別。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# 廣告載入

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**廣告載入**&#x200B;報告維度。 如需如何收集此變數，請參閱[廣告載入型別](/help/implementation/variables/standard-metadata/ad-load-type.md)。*

>[!ENDSHADEBOX]

**廣告載入**&#x200B;維度會報告在每個串流媒體工作階段開始時載入的廣告型別。 此值由客戶定義，可讓組織透過其廣告傳遞機制（例如，`"linear"`、`"dynamic"`或`"programmatic"`）來分類工作階段。

## 如何填入此維度

廣告載入型別由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 設定[[!UICONTROL 串流媒體]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.adLoad`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## 維度項目

每個專案都是工作階段開始時所設定的常值廣告載入型別字串。 值不受限於標準分項清單 — 可定義在您的實施中一致的分類法，以便值可預見地在報表中累計。
