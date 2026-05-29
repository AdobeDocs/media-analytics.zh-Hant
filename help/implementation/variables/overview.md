---
title: 串流媒體變數概觀
description: 瞭解串流媒體變數的組織方式，以及它們如何在Adobe Analytics和Customer Journey Analytics之間對應。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# 串流媒體變數概觀

變數是媒體播放器提供有關資料流的資料，例如內容名稱、資料流型別、廣告名稱和播放品質。 大部分變數會在工作階段開始時設定，並由媒體後端執行至工作階段關閉，系統會使用這些變數填入您在報表中使用的維度和量度。 每個變數頁面都會記錄如何在每個支援的實作方法中設定該變數。

## 如何將變數傳送至Adobe

單一變數會為每個Adobe應用程式或服務傳送相同的值，但該值的格式取決於您傳送該值的位置。 下表列出每個應用程式或服務及其預期的變數格式。 每個變數頁面上的特性表格會顯示要用於每個格式的精確值。

| 資料格式 | 說明 |
| --- | --- |
| 上下文資料變數 | 傳送至Adobe Analytics的格式，以`a.media`首碼命名（例如`a.media.name`）。 |
| XDM集合欄位 | 傳送至Customer Journey Analytics的格式，以XDM欄位路徑表示（例如`xdm.mediaCollection.sessionDetails.name`）。 |
| Audience Manager特徵 | 轉送至Audience Manager的格式，前置詞為`c_contextdata` （例如`c_contextdata.a.media.name`）。 |

>[!MORELIKETHIS]
>
>* [事件總覽](/help/implementation/events/overview.md)：包含變數的播放器事件
>* [維度概觀](/help/reporting/dimensions/overview.md)：變數填入的報告維度
>* [量度總覽](/help/reporting/metrics/overview.md)：變數填入的報告量度
