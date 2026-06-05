---
title: 設定Edge實作的報表
description: 設定Customer Journey Analytics以報告透過Edge Network收集的串流媒體資料。
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# 設定Edge實作的報表

透過Edge Network實作串流媒體收集後，請設定Customer Journey Analytics以報告收集的資料。

>[!NOTE]
>
>本頁涵蓋Customer Journey Analytics中的報告功能，這是Edge實作的建議目的地。 如果您的資料流傳送串流媒體資料給Adobe Analytics，請參閱[為僅限Analytics的實施設定報表](analytics-reporting.md)。

* **必要條件**：完成Edge實作並收集部分資料。 請參閱[Edge實作總覽](/help/implementation/edge/overview.md)以及您選擇的實作方法。

## 在 Customer Journey Analytics 中建立連線

1. 在Customer Journey Analytics中建立連線，如[建立連線](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-connections/create-connection)中所述。 建立連線時，請確定已啟用&#x200B;**[!UICONTROL 匯入所有新資料]**&#x200B;核取方塊。

## 在 Customer Journey Analytics 中建立資料檢視

1. 在Customer Journey Analytics中建立資料檢視，如[建立或編輯資料檢視](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/create-dataview)中所述。

   1. 在&#x200B;**[!UICONTROL 連線]**&#x200B;欄位中，選取您先前建立的連線。 新連線最多可能需要15分鐘才會顯示。

   1. 在&#x200B;**[!UICONTROL 元件]**&#x200B;標籤的&#x200B;**[!UICONTROL 結構描述欄位]**&#x200B;區段中，搜尋下表中每個元件，並將其拖曳至適當的&#x200B;**[!UICONTROL 維度]**&#x200B;或&#x200B;**[!UICONTROL 量度]**&#x200B;面板。 如果存在多個相同名稱的欄位，請使用XDM路徑來確認正確的欄位。 套用元件設定中&#x200B;**[!UICONTROL 內容標籤]**&#x200B;下拉式清單中所顯示的內容標籤。

      | 元件 | 類型 | XDM 路徑 | 內容標籤 |
      |---|---|---|---|
      | [內容](/help/reporting/dimensions/content.md) | 維度 | `mediaReporting.sessionDetails.name` | 媒體：內容ID |
      | [內容名稱](/help/reporting/dimensions/content-name.md) | 維度 | `mediaReporting.sessionDetails.friendlyName` | 媒體：視訊名稱 |
      | [內容長度](/help/reporting/dimensions/content-length.md) | 維度 | `mediaReporting.sessionDetails.length` | 媒體：視訊長度 |
      | [節目](/help/reporting/dimensions/show.md) | 維度 | `mediaReporting.sessionDetails.show` | 媒體：節目 |
      | [季](/help/reporting/dimensions/season.md) | 維度 | `mediaReporting.sessionDetails.season` | 媒體：季數 |
      | [集](/help/reporting/dimensions/episode.md) | 維度 | `mediaReporting.sessionDetails.episode` | 媒體：集數 |
      | 事件型別 | 維度 | `eventType` | 媒體：事件型別 |
      | [內容逗留時間](/help/reporting/metrics/content-time-spent.md) | 量度 | `mediaReporting.sessionDetails.timePlayed` | 媒體：內容逗留時間 |
      | [媒體逗留時間](/help/reporting/metrics/media-time-spent.md) | 量度 | `mediaReporting.sessionDetails.totalTimePlayed` | 媒體：媒體逗留時間 |
      | [總暫停期間](/help/reporting/metrics/total-pause-duration.md) | 量度 | `mediaReporting.sessionDetails.pauseTime` | 媒體：總暫停期間 |
      | [開始時間](/help/reporting/metrics/time-to-start.md) | 量度 | `mediaReporting.qoeDataDetails.timeToStart` | 媒體：開始時間 |
      | [總緩衝期間](/help/reporting/metrics/total-buffer-duration.md) | 量度 | `mediaReporting.qoeDataDetails.bufferTime` | 媒體：總緩衝期間 |
      | 媒體工作階段伺服器逾時 | 量度 | `mediaReporting.sessionDetails.secondsSinceLastCall` | 媒體：自上次呼叫以來的秒數 |

      >[!IMPORTANT]
      >
      >此表格中的內容標籤是串流媒體面板運作所必需的。 Customer Journey Analytics會使用這些量度自動計算&#x200B;**同時檢閱者**&#x200B;和&#x200B;**播放時間**&#x200B;衍生量度（由[媒體同時檢閱者](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)和[媒體播放時間](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)面板使用），並填入[媒體平均每分鐘觀眾數](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)面板的報告選項。

      此時您可以新增任何其他[維度](/help/reporting/dimensions/overview.md)或[量度](/help/reporting/metrics/overview.md)至您的資料檢視。 每個頁面都會列出該元件的XDM路徑。

1. 選取&#x200B;**[!UICONTROL 儲存並繼續]** → **[!UICONTROL 儲存並完成]**&#x200B;以儲存您的變更。

## 在Customer Journey Analytics中建立及設定專案

1. 在Customer Journey Analytics的&#x200B;**[!UICONTROL Workspace]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 專案]**&#x200B;區域中，選取&#x200B;**[!UICONTROL 建立專案]**。

1. 選取&#x200B;**[!UICONTROL 空白專案]** → **[!UICONTROL 建立]**。

1. 在新專案中，選取您先前建立的資料檢視。

   在專案中建立面板時，您可以使用新增至資料檢視的任何元件。

1. 選取左側邊欄中的&#x200B;**面板**&#x200B;圖示，然後拖曳至&#x200B;**[!UICONTROL 媒體平均每分鐘觀眾數]**、**[!UICONTROL 媒體同時檢閱者]**&#x200B;和&#x200B;**[!UICONTROL 媒體播放時間]**&#x200B;面板。

1. （視條件而定）如果您將自訂中繼資料新增到結構描述，請為自訂欄位設定持續性，如Customer Journey Analytics指南中的[持續性元件設定](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)所述。

1. 依照[共用專案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=zh-Hant)中的說明共用專案。

   >[!NOTE]
   >
   >如果您想要共用的使用者無法使用，請確定使用者擁有Adobe Admin Console中Customer Journey Analytics的使用者和管理員存取權。

## Customer Journey Analytics中的可用媒體面板

Customer Journey Analytics中的Analysis Workspace包含三個專用媒體面板，供具有串流媒體收集附加元件的客戶使用。 這些面板會根據最常見的串流媒體報表需求，提供預先建立的視覺效果。

* **[媒體平均每分鐘觀眾數](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**：比較任何長度或型別的節目的平均內容使用量。 支援特定內容（以持續時間為基礎）和自訂時段模式，並允許事後更新持續時間分類。
* **[媒體同時檢閱者](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**：分析一段時間內的同時檢閱者，以找出尖峰同時檢閱和下降點。 支援可設定的粒度和依區段、維度或日期範圍的序列劃分。
* **[媒體播放時間](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**：分析一段時間的播放持續時間，包含尖峰和低谷期間的詳細資料。 支援可設定的詳細程度和輸出格式（小時或分鐘）。

>[!MORELIKETHIS]
>
>* [維度概觀](/help/reporting/dimensions/overview.md)
>* [量度概觀](/help/reporting/metrics/overview.md)
