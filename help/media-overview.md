---
title: Adobe串流媒體概觀
description: 使用Adobe串流媒體解決方案，獲取針對內容、音訊和廣告的強大insight。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 59%

---

# Adobe串流媒體服務總覽

![橫幅](./assets/media_analytics_banner.png)

Adobe串流媒體服務提供適用於串流媒體內容的強大收集、測量和個人化工具，例如適用於串流媒體提供商的音訊、影片和廣告。 您可以將串流媒體量度與Audience Analytics、Mobile或Cross-Device Analytics等功能結合。

串流媒體資料可輕鬆整合至下列Adobe Experience Platform產品：

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>若要實作串流媒體服務，請聯絡您的Adobe銷售代表或Adobe客戶團隊，以確定Customer Journey Analytics串流媒體收集附加元件或Adobe Analytics for Streaming Media附加元件是您產品組合的一部分。

## 主要功能

串流媒體服務的好處包括即時監控、詳細分析、可化為實際行動的深入分析、營利機會等。

* **即時分析**：利用媒體開始時間等關鍵效能量度，在多個管道做出即時決策，以利化為實際行動。

  使用串流媒體服務，您可以對持續時間、停止和開始獲得近乎即時、精細的詳細資訊，讓您能夠評估和組合視訊和音訊量度。 這些見解使您能夠了解客戶的觀看和收聽習慣，並透過高度個人化的推薦提高參與度。

* **促進參與**：透過減少緩衝事件及瞭解廣告在內容中應該播放的時間和位置，提供干擾較少的流暢體驗，促使使用者重複造訪，強化使用者互動。

* **全方位掌握 -** 合併所有內容經銷商的多個資料點，以完整掌控所有媒體活動。測量所有可能管道的參與度和檢視/收聽次數。

  串流媒體服務可讓您追蹤整個網站和串流應用程式的客戶歷程，將客戶路徑和興趣視覺化，並提供強化的推薦和個人化的客戶體驗。  媒體測量可讓您將資料分為多個維度和區段，以擷取完整詳細分析所需的所有中繼資料。如此便能分析資料，並將成功條件歸因於完整使用的媒體、平均逗留時間以及完成的廣告。

* **重要量度**：測量掉格、緩衝時間和平均位元速率等與體驗品質 (QoE) 相關的重要傳送量度。

* **提高詳細程度**：從最精細的層級評估檢視行為，包括個別訪客的每日時間、每分鐘的同時觀眾或聽眾人數以及使用內容的平均持續時間。

* **精準測量**：對使用媒體的多項裝置進行測量，包括 OTT、智慧型手機、平板電腦、桌上型電腦等，以監控使用者的參與模式和習慣。

* **分段**：將分類套用至您的播放器、裝置、類型、章節，並顯示每一種類別如何影響整體的檢視/收聽次數，呈現客戶對內容、音訊、廣告和上述綜合項目的參與度。


## 運作方式

串流媒體服務追蹤資料是使用Media for Edge Network SDK/擴充功能、具有標籤的媒體擴充功能、Media SDK、Media Edge API或媒體收集API從播放器收集的。

所有精細資料 (最多 10 秒) 都會傳送至 Media Analytics Service 或 Experience Edge (取決於您選擇的[實施方法](/help/implementation/overview.md))，它會收集並處理各個播放工作階段的資料。

播放工作階段結束後，會將計算出的追蹤資料傳送至 Adobe Analytics 或 Customer Journey Analytics 進行儲存和報告。

>[!NOTE]
>
>透過 Customer Journey Analytics 實施，可使用 Experience Edge 或使用 Analytics Data Connector (ADC) 將資料傳送至 Customer Journey Analytics。


如需各種實作方法的詳細資訊，請參閱[實作Adobe Analytics或Customer Journey Analytics的串流媒體服務](/help/implementation/overview.md)。
