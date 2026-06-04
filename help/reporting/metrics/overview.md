---
title: 串流媒體量度概觀
description: 瞭解如何在Adobe Analytics和Customer Journey Analytics間計算及組織串流媒體量度。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---


# 串流媒體量度概觀

Streaming Media Analytics中的量度是由媒體後端運算的事件導向計數和持續時間。 媒體播放器會傳送工作階段開始、播放、Ping和廣告開始等事件；媒體後端會處理這些事件，並完成工作階段關閉呼叫上的量度值。

## 量度的計算方式

串流媒體量度遵循四種主要計算模式：

* **事件觸發的旗標**：設定合格事件第一次到達工作階段時。 主要內容的[`play`](/help/implementation/events/playback/play.md)事件設定[[!UICONTROL 內容開始]](content-starts.md)旗標；[`adStart`](/help/implementation/events/ads/ad-start.md)事件設定[[!UICONTROL 廣告開始]](ad-starts.md)。 此旗標會在關閉呼叫時針對每個工作階段報告一次，而非針對每個事件。

* **累積期間**：在特定播放狀態作用中時加總Ping事件之間的間隔。 主要內容播放時會累積[[!UICONTROL 內容逗留時間]](content-time-spent.md)；廣告播放時會累積[[!UICONTROL 廣告逗留時間]](ad-time-spent.md)。 Adobe建議主要內容的Ping間隔為10秒，廣告期間為1秒，因此「逗留時間」量度的精細度必須與實施的Ping間隔相同。

* **事件計數**：追蹤工作階段內的總發生次數。 品品質度，例如[[!UICONTROL 緩衝事件]](buffer-events.md)、[[!UICONTROL 位元速率變更]](bitrate-changes.md)、[[!UICONTROL 錯誤事件]](error-events.md)和[[!UICONTROL 暫停事件]](pause-events.md)會計算每次發生，而不只是第一次發生。

* **受影響的資料流**：如果對應的事件在工作階段期間的任何時間發生，則工作階段層級旗標會設為1，無論發生多少次。 使用這些量度來測量觸及率，同時使用事件計數量度來測量嚴重性。 例如，您可以使用[[!UICONTROL 緩衝影響的資料流]](buffer-impacted-streams.md)來決定所有播放工作階段中受緩衝影響的工作階段比例。

## 依報告系統的可用性

| 報告系統 | 量度如何到達 |
| --- | --- |
| Adobe Analytics | 使用[內容資料變數](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/page-vars/contextdata)填入。 有些量度會使用這些內容資料變數自動填入解決方案事件，而其他量度則必須使用[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)對應至自訂事件。 自動填入值的量度必須先啟用其各自的[串流媒體報表套裝設定](../setup/analytics-reporting.md)。 |
| Customer Journey Analytics | `xdm.mediaReporting.sessionDetails`和相關節點中的XDM欄位，源自任何包含串流媒體資料的資料集。 您必須使用[資料檢視元件設定](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/component-settings/overview)中的所需設定來建立每個量度。 |
| 資料摘要 | 量度在`event_list`和`post_event_list`欄中顯示為事件ID。 每個摘要檔案都包含一個`events.csv`檔案，其中包含所有量度（包括串流媒體量度）的查詢。 |

>[!MORELIKETHIS]
>
>* [事件總覽](/help/implementation/events/overview.md)：填入量度的播放器事件
>* [變數總覽](/help/implementation/variables/overview.md)：事件攜帶到Adobe的資料
>* [維度概觀](/help/reporting/dimensions/overview.md)：變數填入的報告維度
