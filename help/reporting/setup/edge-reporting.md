---
title: 設定Edge實作的報表
description: 設定Customer Journey Analytics以報告透過Edge Network收集的串流媒體資料。
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 17%

---

# 設定Edge實作的報表

透過Edge Network實作串流媒體收集後，請設定Customer Journey Analytics以報告收集的資料。 本頁面說明如何建立串流媒體的連線、資料檢視和專案。

>[!NOTE]
>
>本頁涵蓋Customer Journey Analytics中的報告功能，這是Edge實作的建議目的地。 如果您的資料流傳送串流媒體資料給Adobe Analytics，請參閱[為僅限Analytics的實施設定報表](analytics-reporting.md)。

* **必要條件**：完成Edge實作並收集部分資料。 請參閱[Edge實作總覽](/help/implementation/edge/overview.md)以及您選擇的實作方法。

## 在 Customer Journey Analytics 中建立連線

1. 在Customer Journey Analytics中建立連線，如[建立連線](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hant)中所述。

   建立連線時，串流媒體需要以下選擇：

   1. 選取您在實施期間建立的資料集。

   1. 確定已啟用&#x200B;**[!UICONTROL 匯入所有新資料]**&#x200B;設定。

1. 繼續[在Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics)中建立資料檢視。

## 在 Customer Journey Analytics 中建立資料檢視

1. 在Customer Journey Analytics中建立資料檢視，如[建立或編輯資料檢視](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hant)中所述。

   1. 在&#x200B;**[!UICONTROL 連線]**&#x200B;欄位中，選取您先前建立的連線。

      選取新連線最多可能需要15分鐘。

   1. 在&#x200B;**[!UICONTROL 元件]**&#x200B;標籤的&#x200B;**[!UICONTROL 結構描述欄位]**&#x200B;區段中，搜尋下表中每個元件，並將其拖曳至&#x200B;**[!UICONTROL 量度]**&#x200B;面板。 如果存在多個相同名稱的欄位，請使用XDM路徑來確認正確的欄位。

      **主要內容 — 內容量度**

      | 元件名稱 | XDM 路徑 |
      |----------|---------|
      | 媒體開始次數 | mediaReporting.sessionDetails.isViewed |
      | 媒體區段檢視次數 | mediaReporting.sessionDetails.hasSegmentView |
      | 內容開始 | mediaReporting.sessionDetails.isPlayed |
      | 內容結束 | mediaReporting.sessionDetails.isCompleted |
      | 內容逗留時間 | mediaReporting.sessionDetails.timePlayed |
      | 媒體逗留時間 | mediaReporting.sessionDetails.totalTimePlayed |
      | 不重複播放時間 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10% 進度標記 | mediaReporting.sessionDetails.hasProgress10 |
      | 平均分鐘觀眾數 | mediaReporting.sessionDetails.averageMinuteAudience |

      **章節與廣告 — 章節與廣告量度**

      | 元件名稱 | XDM 路徑 |
      |----------|---------|
      | 章節已開始 | mediaReporting.chapterDetails.isStarted |
      | 章節已完成 | mediaReporting.chapterDetails.isCompleted |
      | 章節時間已播放 | mediaReporting.chapterDetails.timePlayed |
      | 廣告開始 | mediaReporting.advertisingDetails.isStarted |
      | 廣告完成 | mediaReporting.advertisingDetails.isCompleted |
      | 廣告播放時間 | mediaReporting.advertisingDetails.timePlayed |

      **QoE - QoE量度**

      | 元件名稱 | XDM 路徑 |
      |----------|---------|
      | 開始時間 | mediaReporting.qoeDataDetails.timeToStart |
      | 開始前掉格 | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | 緩衝影響的資料流 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | 位元速率變更影響的資料流 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | 位元速率變更 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 平均位元速率 | mediaReporting.qoeDataDetails.bitrateAverage |
      | 掉格 | mediaReporting.qoeDataDetails.droppedFrames |
      | 錯誤 | mediaReporting.qoeDataDetails.errorCount |
      | 錯誤影響的資料流 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | 掉格影響的資料流 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |

      **播放器狀態 — 播放器狀態量度**

      | 元件名稱 | XDM 路徑 |
      |----------|---------|
      | 播放器狀態集 | mediaReporting.states.isSet |
      | 播放器狀態計數 | mediaReporting.states.count |
      | 播放器狀態時間 | mediaReporting.states.time |

   1. 更新下表中元件的標籤（在&#x200B;**[!UICONTROL 內容標籤]**&#x200B;下拉式功能表中）。 搜尋並拖曳量度面板中尚未的任何元件至面板。

      | 元件名稱 | 內容標籤 |
      |---------|----------|
      | 媒體工作階段伺服器逾時 | 媒體：自上次呼叫以來的秒數 |
      | 媒體逗留時間 | 媒體：媒體逗留時間 |
      | 總緩衝期間 | 媒體：總緩衝期間 |
      | 開始時間 | 媒體：開始時間 |
      | 總暫停期間 | 媒體：總暫停期間 |

   1. 若要在專案中加入劃分，請將下列維度加入&#x200B;**[!UICONTROL 維度]**&#x200B;面板：

      | XDM 路徑 | 元件名稱 |
      |---------|----------|
      | mediaReporting.states.name | 播放器狀態名稱 |
      | mediaReporting.sessionDetails.ID | 媒體工作階段 ID |

      除了此表格中的維度之外，您也可以在專案中新增任何其他要用來篩選資料的維度。

1. 選取「儲存並繼續」**[!UICONTROL >「**&#x200B;[!UICONTROL &#x200B;儲存並完成」]&#x200B;**以儲存您的變更。]**

1. 繼續[在Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics)中建立及設定專案。

## 在Customer Journey Analytics中建立及設定專案

1. 在Customer Journey Analytics的&#x200B;**[!UICONTROL Workspace]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 專案]**&#x200B;區域中，選取&#x200B;**[!UICONTROL 建立專案]**。

1. 選取&#x200B;**[!UICONTROL 空白專案]** > **[!UICONTROL 建立]**。

1. 在新專案中，選取您先前建立的資料檢視。

   在專案中建立面板時，您可以使用新增至資料檢視的任何元件。

1. 選取左側邊欄中的&#x200B;**面板**&#x200B;圖示，然後拖曳至&#x200B;**[!UICONTROL 媒體同時檢閱者]**&#x200B;面板和&#x200B;**[!UICONTROL 媒體播放時間]**&#x200B;面板。

1. （視條件而定）如果您將自訂中繼資料新增到結構描述，請為自訂欄位設定持續性，如Customer Journey Analytics指南中的[持續性元件設定](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)所述。

1. 依照[共用專案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)中的說明共用專案。

   >[!NOTE]
   >
   >如果您想要共用的使用者無法使用，請確定使用者擁有Adobe Admin Console中Customer Journey Analytics的使用者和管理員存取權。

>[!MORELIKETHIS]
>
>* Workspace中的[媒體面板](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [維度概觀](/help/reporting/dimensions/overview.md)
>* [量度概觀](/help/reporting/metrics/overview.md)
