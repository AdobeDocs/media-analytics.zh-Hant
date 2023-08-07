---
title: 適用於串流媒體的 Adobe Analytics 概觀
description: 使用適用於串流媒體的 Analytics 獲取對內容、音訊和廣告的強大見解。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# 適用於串流媒體的 Adobe Analytics 概觀

![橫幅](./assets/media_analytics_banner.png)

適用於串流媒體的 Adobe Analytics 可為音訊、視訊和廣告提供功能強大的測量工具。 您可以將串流媒體量度與其他 Adobe Analytics 功能結合使用，例如 Audience Analytics、Mobile 或 Cross-Device Analytics。 

串流媒體可以 Adob&#x200B;&#x200B;e Analytics 附加元件供選購<!-- update this when SKUs are available for other AEP products -->，且串流媒體量度可輕鬆整合至以下 Adob&#x200B;&#x200B;e Experience Platform 產品中：

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>要實施 Adobe Analytics 串流媒體，請聯絡您的 Adobe 銷售代表或 Adobe 帳戶團隊，以確保串流媒體是您產品組合的一部分。

## 主要功能

適用於串流媒體的 Adobe Analytics 具備即時監控、詳細分析、可操作分析和營利商機等多項優勢。

* **即時分析**：利用媒體開始時間等關鍵效能量度，在多個管道做出即時決策，以利化為實際行動。

  借助適用於串流媒體的 Analytics，您可以對持續時間、停止和開始獲得近乎即時、精細的詳細資料，讓您能夠評估和組合視訊和音訊量度。 這些見解使您能夠了解客戶的觀看和收聽習慣，並透過高度個人化的推薦提高參與度。

* **促進參與**：透過減少緩衝事件及瞭解廣告在內容中應該播放的時間和位置，提供干擾較少的流暢體驗，促使使用者重複造訪，強化使用者互動。

* **全方位掌握 -** 合併所有內容經銷商的多個資料點，以完整掌控所有媒體活動。測量所有可能管道的參與度和檢視/收聽次數。

  適用於串流媒體的 Adobe Analytics 可讓您追踪整個網站和串流媒體應用程式的完整客戶歷程，以視覺化方式表達客戶路徑和興趣，並提供增強的建議和個人化客戶體驗。媒體測量可讓您將資料分為多個維度和區段，以擷取完整詳細分析所需的所有中繼資料。如此便能分析資料，並將成功條件歸因於完整使用的媒體、平均逗留時間以及完成的廣告。

* **重要量度**：測量掉格、緩衝時間和平均位元速率等與體驗品質 (QoE) 相關的重要傳送量度。

* **提高詳細程度**：從最精細的層級評估檢視行為，包括個別訪客的每日時間、每分鐘的同時觀眾或聽眾人數以及使用內容的平均持續時間。

* **精準測量**：對使用媒體的多項裝置進行測量，包括 OTT、智慧型手機、平板電腦、桌上型電腦等，以監控使用者的參與模式和習慣。

* **分段**：將分類套用至您的播放器、裝置、類型、章節，並顯示每一種類別如何影響整體的檢視/收聽次數，呈現客戶對內容、音訊、廣告和上述綜合項目的參與度。


## 運作方式

串流媒體追蹤資料是使用 Media for Edge Network SDK/擴充功能、含標記的 Media 擴充功能、Media SDK、Media Edge API 或 Media Collection API 從播放器收集的。

所有精細資料 (最多 10 秒) 都會傳送至 Media Analytics Service 或 Experience Edge (取決於您選擇的[實施方法](/help/implementation/overview.md))，它會收集並處理各個播放工作階段的資料。

播放工作階段結束後，會將計算出的追蹤資料傳送至 Adobe Analytics 或 Customer Journey Analytics 進行儲存和報告。

>[!NOTE]
>
>透過 Customer Journey Analytics 實施，可使用 Experience Edge 或使用 Analytics Data Connector (ADC) 將資料傳送至 Customer Journey Analytics。


有關各種實施方法的詳細資訊，請參閱[為 Adob&#x200B;&#x200B;e Analytics 或 Customer Journey Analytics 實施串流媒體](/help/implementation/overview.md)。
