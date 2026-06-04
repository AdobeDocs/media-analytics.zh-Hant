---
title: 串流媒體維度概觀
description: 瞭解如何填入及組織Adobe Analytics和Customer Journey Analytics中的串流媒體維度。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# 串流媒體維度概觀

串流媒體Analytics中的維度可讓您依內容名稱、串流型別、廣告名稱和其他數十個屬性來切割和篩選量度。 大部分由播放器在工作階段開始時設定，並持續進行到工作階段關閉。

## 維度的填入方式

串流媒體維度遵循三個主要母體模式：

* **由媒體播放器提供**：大多數維度的來源。 播放器會在[工作階段開始](/help/implementation/events/session/session-start.md)呼叫中傳送這些值，而媒體後端會將它們附加到工作階段中的每個後續事件。 播放器在工作階段開始時傳送的是報表中顯示的內容。 範例包括[[!UICONTROL 資料流型別]](/help/reporting/dimensions/stream-type.md)、[[!UICONTROL 內容名稱]](/help/reporting/dimensions/content-name.md)和[[!UICONTROL 內容長度]](/help/reporting/dimensions/content-length.md)。

* **衍生值**：媒體後端從累積播放狀態計算出的維度，而非讀取播放器提供的值的維度。 [[!UICONTROL 內容區段]](/help/reporting/dimensions/content-segment.md)是根據播放過程中的播放點位置計算而得。 [[!UICONTROL 媒體路徑]](/help/reporting/dimensions/media-path.md)在整個工作階段中追蹤內容與廣告狀態之間的轉變。 播放器無法覆寫這些維度。

* **分類**：選擇性。 您可以使用[分類集](https://experienceleague.adobe.com/zh-hant/docs/analytics/components/classifications/sets/overview) (Adobe Analytics)或[查詢資料集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics)來維護分類資料，而不填入個別的維度。

## 依報告系統的可用性

| 報告系統 | 維度如何到達 |
| --- | --- |
| Adobe Analytics | 使用[內容資料變數](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/page-vars/contextdata)填入。 有些維度會使用這些內容資料變數自動填入維度，而其他維度則必須使用[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)填入。 自動填入值的維度必須先啟用其各自的[串流媒體報表套裝設定](../setup/analytics-reporting.md)。 |
| Customer Journey Analytics | XDM欄位通常位於`xdm.mediaReporting.sessionDetails`中，其來源為包含串流媒體資料的任何資料集。 您必須使用[資料檢視元件設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)中的所需設定來建立每個維度。 |
| 資料摘要 | 自動填入的維度有自己的資料摘要欄名稱（如`videostreamtype`、`videoname`或`videolength`）。 需要處理規則的維度使用`evar`欄名稱。 |
| Audience Manager | 從Adobe Analytics轉送的內容資料。 只有在已設定Analytics至Audience Manager伺服器端轉送時才能使用。 |

>[!MORELIKETHIS]
>
>* [事件總覽](/help/implementation/events/overview.md)：填入維度的播放器事件
>* [變數總覽](/help/implementation/variables/overview.md)：事件攜帶到Adobe的資料
>* [量度總覽](/help/reporting/metrics/overview.md)：變數填入的報告量度
