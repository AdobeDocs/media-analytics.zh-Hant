---
title: 媒體同時檢閱者
description: 「了解用來顯示一整天的同時檢閱者的『媒體同時檢閱者』控制面板。 您可依內容、裝置類型或國家/地區來篩選資料。」
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: "Media Analytics, Reports & Analytics Basics"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '291'
ht-degree: 100%

---

# 媒體同時檢閱者報表 {#media-concurrent-viewers}

「媒體同時檢閱者」控制面板會顯示一天內同時檢視媒體的使用者。您可依內容、裝置類型或國家/地區來篩選這項資料。

>[!TIP]
>
> 此報表主要是以同時作用的媒體工作階段為基礎編撰而成。若要依不重複訪客檢視同時檢閱的情形，並使用套用區段、劃分及比較數據等其他功能，請使用 [Analysis Workspace 的「媒體同時檢閱者」面板](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=zh-Hant)。

![](assets/video-concurrent-viewers.png)

## 報表特色 {#report-features}

此報表的部分特色如下：

* 並非即時產生。如同 Adobe Analytics 一樣會有正常延遲。
* 報表時段橫跨 24 小時。X 軸是以報表套裝時區為基礎的當日時間。
* 報表會以分鐘為單位顯示同時檢閱者。
* *媒體同時檢閱者報表*&#x200B;會顯示正在觀看或聆聽內容的人數。
* 媒體同時檢閱者報表內的&#x200B;*「媒體詳細資訊」*&#x200B;報表會顯示正在觀看或聆聽特定媒體項目的人數。
* 報表僅能呈現一天的數據。
* 客戶可檢視同時檢閱者歷史報表 (以天為單位瀏覽)。

## 限制 {#limitations}

此報表的部分限制如下：

* 若選擇的間隔並非一整天，資料將不會顯示。
* 無法匯出 ReportBuilder 等資料。
* 資料無法以表格格式呈現。
* 報表無法透過電子郵件傳送。
* 即使不追蹤廣告，也必須重新啟用媒體追蹤功能，並選取媒體廣告模組。
* 心率資料庫必須具備暫停追蹤功能，此功能才有辦法提供精確資料。
