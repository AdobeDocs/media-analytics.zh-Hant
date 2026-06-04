---
title: 媒體路徑
description: 擷取內容ID作為流量變數，以進行路徑分析。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# 媒體路徑

**媒體路徑**&#x200B;維度會擷取內容ID做為流量變數(prop)，以便用於路徑分析（例如，下一個內容和上一個內容流量報表）。 這是Adobe Analytics獨有的： Customer Journey Analytics不會儲存流量變數，而路徑會直接在內容(ID)維度上執行。

## 如何填入此維度

媒體路徑會自動衍生自工作階段開始時設定的內容ID。 沒有要設定的個別變數；只要填入內容(ID)，就會填入資料摘要資料行`videopath`。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 媒體核心]](/help/reporting/setup/analytics-reporting.md)時，自動從內容資料`a.media.name`收集為流量變數(prop)。 |
| Customer Journey Analytics | 不適用 — 使用[Content](content.md)進行路徑分析 |
| 資料饋送 | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Adobe Analytics prop有100個位元組的限制。 超過100個位元組的值會遭到截斷。

>[!IMPORTANT]
>
>路徑報表會比較同一次造訪中不同點選的prop值。 如果內容(ID)在造訪中變更（例如，當檢視者從一段內容移至另一段內容時），路徑報表會顯示該流量。

## 維度項目

每個專案都是造訪期間報告的內容ID。 使用Adobe Analytics中「內容>媒體路徑」底下的「下一頁流量」和「上一頁流量」報表，檢視內容對內容的導覽路徑。
