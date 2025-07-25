---
title: 啟用媒體報表
description: 了解收集媒體量度的媒體報表套裝。 遵循這些步驟，在傳送媒體資料之前設定媒體報表。
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 98%

---

# 啟用媒體報表{#media-reports-enablement}

在傳送媒體資料之前，必須先設定好收集媒體量度的每個報表套裝。

>[!TIP]
>
>若要利用新功能，現有的串流媒體客戶應該為他們的RSID重新啟用媒體追蹤。

1. 在 [Adobe Analytics](https://experience.adobe.com) 中，按一下&#x200B;**[!UICONTROL 「管理員」>「報表套裝」]。**
1. 選取您要收集媒體資料的報表套裝，然後按一下&#x200B;**[!UICONTROL 「編輯設定」>「媒體管理」>「媒體報表」]。**

   ![](assets/media-reporting.png){width="400px"}

1. 在&#x200B;**[!UICONTROL 「媒體報表」]**&#x200B;頁面上，啟用&#x200B;**[!UICONTROL 「媒體核心」]**，並選擇性地啟用 **[!UICONTROL 「媒體廣告」]、** **[!UICONTROL 「媒體章節」],**&#x200B;和&#x200B;**[!UICONTROL 「媒體品質」]**。

   媒體測量包含下列模組:

   * **媒體核心**

     核心媒體測量可用於測量媒體內容。這將使用解決方案 (或自訂) eVar 來保持追蹤內容、內容類型、內容播放器名稱和內容頻道。解決方案 (或自訂) 事件將用於媒體開始、內容開始、內容結束和內容逗留時間。

   * **媒體廣告**

     媒體廣告測量用於媒體內容內廣告的測量。這將使用解決方案 eVar 來測量廣告、廣告播放器名稱、廣告 Pod 和 Pod 位置中的廣告。解決方案事件將用於廣告開始、廣告完成、廣告逗留時間和視訊逗留時間。

   * **媒體章節**

     視訊章節測量用於章節的測量。章節是單一媒體中內容的細分。這將使用解決方案 eVar 來儲存章節 ID。解決方案事件將用於章節開始、章節完成、章節逗留時間。將提供章節名稱和章節位置的其他章節中繼資料做為章節 ID 的分類。

   * **媒體品質**

     視訊品質測量將用於測量內容播放的品質。這將使用解決方案 eVar 來儲存開始時間、緩衝事件、緩衝時間長度總計、位元速率參數、平均位元速率、錯誤及掉格。解決方案事件將用於：開始時間、開始前掉格、緩衝影響的資料流、緩衝事件、緩衝時間長度總計、位元速率變更影響串流、位元速率變更、平均位元速率、錯誤影響、錯誤事件、掉格影響的資料流，以及掉格。

   * **視訊與視訊廣告中繼資料**

     中繼資料可附加至媒體和/或廣告，以便進一步說明該媒體/廣告並加以分類。標準化媒體及廣告中繼資料是透過解決方案變數及分類所收集而得。這些值包含:「節目」、「季數」、「集數」、「資產 ID」、「類型」、「首播日期」、「首次數位化日期」、「內容評等」、「創作者」、「網路」、「節目類型」、「廣告載入」、「MVPD」、「已授權」、「播出時段」、「媒體工作階段 ID」、「廣告商」、「促銷活動 ID」及「創作 ID」。

   * **音訊和音訊廣告中繼資料**

     可以將中繼資料附加至音訊和/或廣告，以進一步描述並分類該音訊/廣告。標準化的音訊和廣告中繼資料將會透過解決方案變數和分類收集。包含的值為: 藝人、專輯、標籤、作者、出版社、電視台、節目、季數、集數、資產 ID、類型、首播日期、首次數位化日期、內容評等、創作者、網路、節目類型、廣告載入、MVPD、已授權、時段、媒體工作階段 ID、廣告商、促銷活動 ID 以及創作 ID。

   啟用每個模組會保留一組變數，並建立一組新的報表。由於品質的例外情況，除非已完成對應的實施，否則報表中將不會有資料。如果有啟用，實施核心模組也會實施品質模組。

   如果您尚未追蹤廣告、章節或播放品質，您可以隨時啟用其他選項。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]。**

   若此報表套裝已設定來收集媒體資料，在您按一下&#x200B;**[!UICONTROL 「儲存」]**&#x200B;後，將顯示另一個設定頁面。如果您看見&#x200B;**[!UICONTROL 「媒體核心測量」]**&#x200B;頁面，請繼續進行下一個步驟。

1. (條件式) 在&#x200B;**[!UICONTROL 「媒體核心測量」]**&#x200B;頁面上，選擇繼續使用自訂變數或選擇使用解決方案變數。

   | 選項 | 附註 |
   | --- | --- |
   | 繼續使用自訂變數 | 優點與缺點:<ul> <li> **優點:** 內容趨勢會在移轉之後繼續運作。 </li> <li> **缺點:** 需要您保持配置給媒體兩個自訂的 eVar 和三個自訂事件。您會重新獲得一個自訂 eVar 和一個自訂事件的使用。 </li> </ul> 若要繼續使用自訂變數： <ol> <li>選取&#x200B;**[!UICONTROL 「使用自訂變數」]**，然後按一下&#x200B;**[!UICONTROL 「儲存」]**。 </li> <li>出現提示時，對映您目前的自訂 eVar 和事件，然後按一下&#x200B;**[!UICONTROL 「儲存」]**: </li> </ol> |
   | 移轉至解決方案變數 | 優點與缺點:<ul> <li> **優點：**&#x200B;您會重新獲得三個自訂 eVar 和四個自訂事件的使用。 </li> <li> **缺點：**&#x200B;您會遺失媒體報表的&#x200B;**所有**&#x200B;歷史趨勢和比較。這表示在移轉至心率之前，您無法追蹤任何日期的內容檢視或內容播放時間。 </li> </ul> **限制:** 請勿移轉至解決方案變數，除非您確定不要保留此趨勢。所有客戶應只在他們需要保留歷史持續性時，才使用解決方案變數及處理規則，將媒體資料放置到現有的 prop 和 eVar。若要移轉至解決方案變數: 選取&#x200B;**[!UICONTROL 「使用解決方案變數」]**，然後按一下&#x200B;**[!UICONTROL 「儲存」]。** <br><br> 重要: 移轉至解決方案變數會造成您遺失媒體報表的&#x200B;**所有**&#x200B;歷史趨勢和比較。 |

>[!IMPORTANT]
>
>請勿變更量度和中繼資料表格所列之任何變數的分類名稱 (例如[音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md))，其說明以「分類」形式顯示於「報表/保留變數」下方。為媒體追蹤啟用報表套裝時，系統會定義媒體分類。Adobe 有時會新增屬性，而發生這種情形時，客戶必須重新啟用其報表套裝才能存取新的媒體屬性。在更新程序期間，Adobe 會檢查變數名稱，藉此決定是否啟用分類。如果有任何變數名稱遺失，Adobe 會再次新增遺失的項目。
