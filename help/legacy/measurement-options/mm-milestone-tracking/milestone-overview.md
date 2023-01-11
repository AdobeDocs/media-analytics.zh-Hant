---
title: 了解里程碑報告 (已過時)
description: 已過時 - 了解如何為里程碑的實作設定視訊報告
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356ccc5
exl-id: 960785e3-f507-4f09-8f85-6eeca57dd2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '3349'
ht-degree: 100%

---

# 里程碑概觀{#milestone-overview}

>[!CAUTION]
>
>這個測量選項已過時。

[舊版里程碑文件](milestone_analytics_video.pdf)

## 設定 {#configuration}

### 里程碑視訊設定

若要追蹤視訊，請指定一組要用來追蹤及報告的「自訂轉換變數」**(eVar) 與「自訂事件」**。路徑功能還會使用一個「自訂分析」**&#x200B;變數 (`s.prop`

您對每個量度選取的變數會新增至視訊設定頁面。這會讓系統自動產生和格式化標準視訊報表。*視訊名稱* eVar 和&#x200B;*視訊檢視*&#x200B;計數器均為必要。其他變數為選用變數，但如需完整測量則建議使用。啟用視訊追蹤之後，您可以檢視從您使用視訊追蹤報表的視訊資料所產生的報表。

您也可以對視訊追蹤任何數量的其他量度。例如，如果在您的網站上使用多個視訊播放器，可以填入具有播放器名稱的 eVar。您選取的部分變數可能也會用於網站的其他區域。例如，如果是在整個網站上使用，*內容類型*&#x200B;變數可讓您測量來自視訊的頁面檢視的百分比，並讓您將轉換事件與視訊產生關連。

### 里程碑報表設定

若要設定「里程碑」實作的視訊報表，請前往&#x200B;**[!UICONTROL 「管理員 > 報表套裝管理器」]。**&#x200B;選取報表套裝，然後選擇&#x200B;**[!UICONTROL 「視訊管理 > 視訊報表」]：**

<!--
![](assets/0clip_image002_1537416456.png){width="248"}
-->

![](assets/rs1.png)

第一個畫面，只有「視訊核心」可搭配「里程碑」中繼資料使用。選取&#x200B;**[!UICONTROL 「視訊核心」]**，然後按一下&#x200B;**[!UICONTROL 「儲存」]。**

![](assets/video-core-check.png)

在下一個畫面，選取&#x200B;**[!UICONTROL 「使用自訂變數」]**。

<!--
![](assets/0clip_image006_-1561510960.png){width="470"}
-->

![](assets/rs2.png)

在最後一個畫面，選取要搭配視訊測量使用的兩個 eVar 和三個事件：

<!--
![](assets/0clip_image008_-92166399.png)
-->

![](assets/rs3.png)

## 視訊變數參考資料 {#video-variable-reference}

下表包含視訊的商務變數和自訂事件的其他詳細資料：

| 視訊量度 | 變數類型 | 說明 |
| --- | --- | --- |
| 內容 | eVar <br/>預設過期時間：造訪 | (必要) 依實作指示收集視訊名稱。 |
| 內容類型 | eVar <br/>預設過期時間：頁面檢視 | 收集訪客所檢視內容類型的相關資料。視訊測量傳送的點擊會被指派為 `video.` 的內容類型。<br/>不需專為視訊追蹤保留此變數。使用此相同變數而具有其他內容報表內容類型，可讓您分析不同內容類型中訪客的分佈情況。舉例來說，使用了這個變數，您就可以利用像是 `article` 或 `product page` 等值來標記其他內容類型。<br/>從視訊測量觀點，「內容類型」**&#x200B;可讓您識別視訊訪客，並因此計算視訊轉換率。 |
| 內容逗留時間 | 事件<br/>類型：計數器 | 計算自上次資料收集程序 (影像要求) 以來，用於觀看視訊的時間 (以秒為單位)。 |
| 視訊起始 | 事件<br/>類型：計數器 | 指出有訪客檢視了視訊的某部分。但此量度並不會針對訪客所檢視的視訊提供任何關於檢視內容的多少、哪一部分的資訊。 |
| 視訊完成 | 事件<br/>類型：計數器 | 指出使用者已檢視完整的視訊。預設情況下，完成事件會在視訊結尾之前 1 秒測量。<br/>實作期間，您可以指定想要將距離視訊結尾幾秒視為檢視完成。針對即時視訊和沒有已定義結尾的其他資料流，您可以指定測量完成的自訂點。例如，在特定檢視次數之後。 |

## 媒體模組變數 {#media-module-variables}

下列變數可讓您設定視訊測量。您必須為在「必要變數」表格中的變數定義值。此外，若要追蹤您的視訊播放器中的事件，您必須使用開啟、播放、停止和關閉方法來啟用 autoTrack (針對支援的播放器)，或實作自訂播放器事件追蹤。

| 變數 | 說明 |
| --- | --- |
| `Media.trackUsingContextData` | **語法：** <br/><br/> `s.Media.trackUsingContextData = true;`<br/>此選項可啟用整合式視訊追蹤。設為 true 時，媒體模組會為媒體追蹤產生內容資料，而不是舊版 `pev3`。<br/>使用 `Media.contextDataMapping` 來對應內容資料至選取的 eVar 和事件。<br/>預設值：`false` |
| `Media.contextDataMapping` | **語法：** <br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};`<br/><br/>一個物件，定義您要用於視訊測量的變數對應至 eVar 和事件。物件必須對應下列欄位：<br/><br/> **a.media.name：**(必要) 以視訊名稱填入變數。提供您選取要儲存視訊名稱的 eVar，以及要用於視訊路徑的「自訂分析視訊」變數 (`s.prop`)。以逗號分隔的清單提供值。<br/><br/> **a.media.segment：**(選用) 您要儲存媒體區段名稱的 eVar。a.contentType：(選用) 您要儲存視訊值的 eVar，其包含已啟用的造訪和訪客追蹤，用以產生視訊造訪和訪客報表。您選取的變數似乎已用來儲存文章投影片放映或產品頁面之類的資料 <br/><br/> **a.media.view：**(必要) 您要計算媒體檢視次數的事件。<br/><br/> **a.media.segmentView：**(選用) 您要計算區段檢視次數的事件。<br/><br/> **a.media.complete：**(選用) 您要計算完整檢視次數的事件。<br/><br/> **a.media.timePlayed：**(選用，強烈建議使用) 您要儲存播放的視訊秒數的數值事件。<br/><br/> **a.media.milestones：**(選用) 將 s.Media.trackMilestones 里程碑與計數器事件對應的物件。如果您定義里程碑，Media.segmentByMilestones 應該設為 true。<br/><br/> **廣告追蹤** 若要追蹤廣告，可使用下列內容資料變數：<br/> **a.media.ad.name：**(必要) 以廣告名稱填入變數。提供您選取要儲存廣告名稱的 eVar，以及要用於路徑的「自訂分析視訊」變數 (`s.prop`)。以逗號分隔的清單提供值。<br/><br/> **a.media.ad.pod：**&#x200B;主要內容中播放廣告的位置。<br/><br/> **a.media.ad.podPosition：** Pod 內播放廣告的位置。<br/><br/> **a.media.ad.CPM：**&#x200B;套用至此播放的 CPM 或加密的 CPM (首碼為「~」)。<br/><br/> **A.media.ad.view：**&#x200B;與 `a.media.view` 的作用相同。<br/><br/> **a.media.ad.clicked：**&#x200B;計算廣告點擊次數 (`Media.click` 呼叫次數)<br/><br/> **a.media.ad.timePlayed：**&#x200B;與 `a.media.timePlayed` 的作用相同。<br/><br/> **a.media.ad.complete：** 與 `a.media.complete` a.media.ad.segment 的作用相同：與 `a.media.segment` 的作用相同<br/><br/> **a.media.ad.segmentView：**&#x200B;與 `a.media.segmentView` 的作用相同。<br/><br/> **a.media.ad.milestones：** 與 `a.media.milestones` 的作用相同。<br/><br/> **a.media.ad.offsetMilestones：** 與 `a.media.offsetMilestones` 的作用相同。 |
| `Media.trackVars` | **語法：** <br/><br/> `s.Media.trackVars =` <br/>    `"events,` `prop2,` `eVar1,` `eVar2,` `eVar3";` <br/><br/>在您的視訊追蹤程式碼中設定的所有變數以逗號分隔的清單。  |
| `Media.trackEvents` | **語法：** <br/><br/> `s.Media.trackEvents =` <br/>    `"event1,` `event2,` `event3,` `event4,` `event5,` `event6,` `event7"` <br/><br/>在您的視訊追蹤程式碼中設定的所有事件以逗號分隔的清單。 |

## 選擇性變數 {#optional-variables}

|  變數 | 說明 |
| --- | --- |
| `Media.autoTrack` | **語法：** <br/><br/> `s.Media.autoTrack = true`<br/><br/>啟用對支援的播放器的自動追蹤。支援的播放器如下所示： <ul> <li> Open Source Media Framework (OSMF) </li> <li> FLVPlayback (透過 Flash Professional 中的匯入視訊精靈建立的視訊播放器) </li> <li> Silverlight </li> <li> MediaDisplay </li> <li> MediaPlayback </li> <li> Brightcove API 版本 2 與 3 (請參閱 [Brightcove](https://integrations.support.brightcove.com/adobe/adobe-aem-brightcove-connector-using-connector.html) </li> <li> 使用 JavaScript 的 Windows Media Player、Quicktime 或 Real Player </li> </ul> <br/><br/>如果您未使用以上任一個播放器，則可以使用 `Media.open` `Media.play` `Media.stop` `Media.close` 來追蹤播放器事件。 |
| `Media.autoTrackNetStreams` | **語法：** <br/><br/> `s.Media.autoTrackNetStreams = true`<br/><br/>Flash 10.3 推出 NetStream 元件的新功能，可啟用進階視訊追蹤。如果您使用自訂 Flash NetStream 播放器，則可以啟用此變數以啟用類似於 autoTrack 的功能。此方法要求在 Flash 10.3 或更新版本中檢視視訊。 |
| `Media.completeByCloseOffset` | **語法：** <br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true`<br/><br/>此設定可讓您在視訊實際結束之前幾秒計算所完成的視訊檢視。<br/><br/>會根據 `completeCloseOffsetThreshold` 中指定的秒數來傳送事件。這可讓您在從不會報告等於視訊長度的位移的視訊播放器中測量完成。<br/><br/>預設情況下，此值會設為 true，而臨界值設為 1 秒。有了這些預設值，完成事件會在視訊結尾之前 1 秒傳送。 |
| `Media.completeCloseOffsetThreshold` | **語法：** <br/><br/> `s.Media.completeCloseOffsetThreshold = 1`<br/><br/>此臨界值可讓您在視訊實際結束之前幾秒計算所完成的視訊檢視。必須將 `Media.completeByCloseOffset` 設為 true，才能使用此臨界值。<br/><br/>您提供的整數值會決定位移可以距離視訊長度關閉處，仍被計為完成的秒數。這可讓您在從不會報告等於視訊長度的位移的視訊播放器中測量完成。<br/><br/>預設臨界值為 1 秒。 |
| `Media.playerName` | **語法：** <br/><br/> `s.Media.playerName = "Custom Player Name"`<br/><br/>指定自訂視訊播放器名稱。 |
| `Media.trackSeconds` | **語法：** <br/><br/> `s.Media.trackSeconds = 15`<br/><br/>以秒數定義間隔，用於在視訊播放時傳送視訊追蹤資料至 Adobe 資料收集伺服器。值必須設定為 5 秒的增量。<br/><br/>僅對 `Media.trackSeconds` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 Media.monitor。 |
| `Media.trackMilestones` | 以視訊長度的百分比追蹤里程碑。<br/><br/> **語法：** <br/><br/> `s.Media.trackMilestones = "25, 50, 75";`<br/><br/>以視訊長度的百分比定義間隔，用於傳送視訊追蹤資料至 Adobe 資料收集伺服器。以整數、逗號分隔的清單指定里程碑。例如：10 = 10%，23 = 23%。<br/><br/>因為這些里程碑在視訊中是固定的點，如果訪客檢視超過 10% 里程碑，然後倒轉並再次超過 10% 里程碑，媒體模組會傳送多次追蹤資料。類似地，如果訪客快轉超過某個里程碑，媒體模組不會為該里程碑傳送追蹤資料。<br/><br/>僅對 `Media.trackMilestones` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 Media.monitor。 |
| `Media.trackOffsetMilestones` | 以從視訊開始的經過秒數來追蹤里程碑。<br/><br/> **語法：** <br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";`<br/><br/>以從視訊開始的經過秒數定義間隔，用於傳送視訊追蹤資料至 Adobe 資料收集伺服器。以整數、逗號分隔的清單指定里程碑。例如：20 = 20 秒，40 = 40 秒。<br/><br/>因為這些里程碑在視訊中是固定的點，如果訪客檢視超過里程碑 20 秒，然後倒轉並再次超過 20 秒里程碑，媒體模組會傳送多次追蹤資料。類似地，如果訪客快轉超過某個里程碑，媒體模組不會為該里程碑傳送追蹤資料。<br/><br/>僅對 `Media.trackOffsetMilestones` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 Media.monitor。 |
| `Media.segmentByMilestones` | **語法：** <br/><br/> `s.Media.segmentByMilestones = true;` <br/><br/>根據 `Media.trackMilestones` 中指定的媒體和里程碑的長度，自動產生區段名稱、區段號碼和區段長度資料。<br/><br/>使用 `autoTrack` 時，依里程碑劃分是定義區段的唯一方式。<br/><br/>預設值：`false` |
| `Media.segmentByOffsetMilestones` | **語法：** <br/><br/> `s.Media.segmentByOffsetMilestones = true;` <br/><br/>根據 `Media.trackOffsetMilestones` 中指定的媒體和里程碑的長度，自動產生區段名稱、區段號碼和區段長度資料。<br/><br/>使用 `autoTrack` 時，依里程碑劃分是定義區段的唯一方式。<br/><br/>預設值：`false` |

## 廣告追蹤變數 {#ad-tracking-variables}

這些變數用來結合 openAd 方法傳送廣告資訊。請參閱 [VAST 視訊廣告追蹤](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)。

| 變數 | 說明 |
| --- | --- |
| `Media.adTrackSeconds` | **語法：** <br/><br/> `s.Media.adTrackSeconds = 15;`<br/><br/>以秒數定義間隔，用於在視訊播放時傳送視訊廣告追蹤資料至 Adobe 資料收集伺服器。值必須設定為 5 秒的增量。<br/><br/>僅對 `Media.adTrackSeconds` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 `Media.monitor`。 |
| `Media.adTrackMilestones` | 以廣告長度的百分比追蹤廣告里程碑。 <br/><br/> **語法：** <br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";`<br/><br/>以廣告長度的百分比定義間隔，用於傳送廣告追蹤資料至 Adobe 資料收集伺服器。以整數、逗號分隔的清單指定里程碑。例如：10 = 10%，23 = 23%。<br/><br/>因為這些里程碑在廣告中是固定的點，如果訪客檢視超過 10% 里程碑，然後倒轉並再次超過 10% 里程碑，媒體模組會傳送多次追蹤資料。類似地，如果訪客快轉超過某個里程碑，媒體模組不會為該里程碑傳送追蹤資料。<br/><br/>僅對 `Media.adTrackMilestones` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 `Media.monitor`。 |
| `Media.adTrackOffsetMilestones` | 以從廣告開始的經過秒數來追蹤廣告里程碑。<br/><br/> **語法：** <br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";`<br/><br/>以從廣告開始的經過秒數定義間隔，用於傳送廣告追蹤資料至 Adobe 資料收集伺服器。以整數、逗號分隔的清單指定里程碑。例如：20 = 20 秒，40 = 40 秒。<br/><br/>因為這些里程碑在廣告中是固定的點，如果訪客檢視超過里程碑 20 秒，然後倒轉並再次超過 20 秒里程碑，媒體模組會傳送多次追蹤資料。類似地，如果訪客快轉超過某個里程碑，媒體模組不會為該里程碑傳送追蹤資料。<br/><br/>僅對 `Media.adTrackOffsetMilestones` 中定義的事件啟用 `Media.contextDataMapping` 觸發。除了為視訊測量指定的這些以外，若要傳送其他變數，您必須使用 `Media.monitor`。 |
| `Media.adSegmentByMilestones` | **語法：** <br/><br/> `s.Media.adSegmentByMilestones = true;` <br/><br/>根據 `Media.adTrackMilestones` 中指定的媒體和里程碑的長度，自動產生區段名稱、區段號碼和區段長度資料。<br/><br/>使用 `autoTrack` 時，依里程碑劃分是定義區段的唯一方式。<br/><br/>預設值：`false` |
| `Media.adSegmentByOffsetMilestones` | **語法：** <br/><br/> `s.Media.adSegmentByOffsetMilestones = true;` <br/><br/>根據 `Media.adTrackOffsetMilestones` 中指定的媒體和里程碑的長度，自動產生區段名稱、區段號碼和區段長度資料。<br/><br/>使用 `autoTrack` 時，依里程碑劃分是定義區段的唯一方式。<br/><br/>預設值：`false` |

## 媒體模組方法 {#media-module-methods}

媒體模組方法可用來手動追蹤播放器事件和追蹤不屬於標準視訊報表的其他度量。

如果您使用 `Media.autoTrack`，並且未追蹤 其他度量，則不需要直接呼叫這些方法的任一個。除非指定為選用，否則所有引數都為必要。

| 方法 | 說明 |
| --- | --- |
| `Media.open` | **語法：** <br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)`<br/><br/>準備用來收集視訊追蹤資料的媒體模組。此方法會採用下列參數： <ul><li> **mediaName：**(必要) 您要其顯示在視訊報表中的名稱。 </li><li>  **mediaLength：**(必要) 視訊的長度 (以秒為單位)。  </li><li> **mediaPlayerName：**(必要) 用來檢視視訊的媒體播放器名稱，您要其顯示在視訊報表中的名稱。 </li></ul> |
| `Media.openAd` | **語法：** <br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>   `parentPod, parentPodPosition, CPM)` <br/><br/>準備用來收集廣告追蹤資料的媒體模組。此方法會採用下列參數： <ul> <li> **name：**(必要) 廣告的名稱或 ID。  </li> <li> **length：**(必要) 廣告的長度。  </li> <li> **playerName：**(必要) 用來檢視廣告的媒體播放器的名稱。  </li> <li> **parentName：**&#x200B;內嵌廣告所在主要內容的名稱或 ID。  </li> <li> **parentPod：**&#x200B;主要內容中播放廣告的位置。  </li> <li> **parentPodPosition：** Pod 內播放廣告的位置。  </li> <li> **CPM：**&#x200B;套至用此播放的 CPM 或加密的 CPM (首碼為 &quot;~&quot;)。  </li> </ul> |
| `Media.click` | **語法：** <br/><br/> `s.Media.click(name, offset)`<br/><br/>追蹤何時在視訊中點按了廣告。此方法會採用下列參數： <ul> <li> **name：**&#x200B;廣告的名稱。這必須符合 Media.openAd 中使用的名稱。  </li> <li> **offset：**&#x200B;發生按一下時進入廣告的位移。  </li> </ul> |
| `Media.close` | **語法：** <br/><br/> `s.Media.close(mediaName)`<br/><br/>結束視訊資料收集並傳送資訊至 Adobe 資料收集伺服器。在視訊結束時呼叫此方法。此方法會採用下列參數： <br/><br/> **mediaName：**&#x200B;視訊的名稱。這必須符合 `Media.open` 中使用的名稱。 |
| `Media.complete` | **語法：** <br/><br/> `s.Media.complete(name, offset)`<br/><br/>此方法會手動追蹤完成的事件。當您需要觸發無法使用`Media.completeByCloseOffset` 處理的特殊邏輯事件時，會使用此方法。<br/><br/>例如，如果您要測量未定義結尾的即時資料流，則可以在使用者檢視即時資料流 X 秒後觸發完成。您可能會根據內容的長度和類型，使用百分比計算來測量完成情形。此方法會採用下列參數： <ul> <li> **mediaName：**&#x200B;視訊的名稱。這必須符合 Media.open 中使用的名稱。  </li> <li> **mediaOffset：**&#x200B;視訊中應該傳送完成事件的秒數。根據從零秒開始的視訊指定位移。<br/><br/>如果您的媒體播放器使用毫秒追蹤，在呼叫 Media.complete 之前，請確定值轉換為秒。  </li> </ul> 如果您計劃手動呼叫完成，請設定 <br/><br/> `s.Media.completeByCloseOffset = false`。 |
| `Media.play` | **語法：** <br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)`<br/><br/>在視訊開始播放對隨時可呼叫此方法。使用手動視訊測量時，您可以在傳送視訊測量資料時提供目前的區段資料。<br/><br/>如果您的播放器因任何原因從一個區段變更為另一個，則應呼叫 `Media.stop` `Media.play`。<br/><br/>此方法會採用下列參數：<br/><br/> **mediaName：**&#x200B;視訊的名稱。這必須符合 Media.open 中使用的名稱。  <br/><br/> **mediaOffset：**&#x200B;視訊中開始播放的秒數。根據從零秒開始的視訊指定位移。如果您的媒體播放器使用毫秒追蹤，在呼叫 Media.play 之前，請確定值轉換為秒。  <br/><br/> **segmentNum：**(選用) 目前的區段號碼，行銷報表用來在報表中排序顯示區段。segmentNum 參數必須大於零。  <br/><br/> **segment：**(選用) 目前的區段名稱。<br/><br/> **segmentLength：**(選用) <br/><br/>目前的區段長度 (以秒為單位)。<br/><br/>例如：<br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **語法：** <br/><br/> `s.Media.stop(mediaName, mediaOffset)`<br/><br/>追蹤指定的視訊的停止事件 (停止、暫停等等)。此方法會採用下列參數： <ul> <li> **mediaName：**&#x200B;視訊的名稱。這必須符合 `Media.open` 中使用的名稱。  </li> <li> **mediaOffset：**&#x200B;視訊中發生停止或暫停事件的秒數。根據從零秒開始的視訊指定位移。  </li> </ul> |
| `Media.monitor` | **語法：** <br/><br/> `s.Media.monitor(s, media)` <br/><br/> **Silverlight 語法：** <br/><br/> `s.Media.monitor =` <br/>   `new AppMeasurement_Media_Monitor(myMediaMonitor);` <br/><br/>Silverlight 應用程式媒體監視會實作 Objective-C 委派設計模式。`myMediaMonitor` 類別方法採用 `s` 和 `media` 參數。<br/><br/>使用此方法來傳送其他視訊測量。您可以設定其他變數 (Prop、eVar、事件)，並在播放視訊時根據視訊的目前狀態，使用 `Media.track` 傳送它們。<br/><br/>請參閱[使用 Media.monitor 測量其他度量。](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=zh-Hant) <br/><br/>此方法會採用下列參數：<br/><br/>  **s：**`AppMeasurement` 例項 (或 JavaScript `s` 物件)。<br/><br/> **media：**&#x200B;物件，其成員提供視訊的狀態。這些成員包括：  <ul><li> `media.name:` 視訊的名稱。這必須符合 `Media.open` 中使用的名稱； </li><li> `media.length:` 在對 `Media.open` 的呼叫中提供的視訊的長度 (以秒為單位)； </li><li> `media.playerName:` 在對 `Media.open` 的呼叫中指定的媒體播放器名稱； </li><li> `media.openTime:` 包含呼叫 `Media.open` 時資料的 NSDate 物件； </li><li> `media.offset:` 進入視訊的目前位移 (以秒為單位) (視訊中的實際點)。位移從零開始 (視訊的第一個秒數為 0 秒)； </li><li> `media.percent:` 目前已播放視訊的百分比，根據視訊長度和目前的位移；  </li><li> `media.timePlayed:` 目前播放的總秒數；  </li><li> `media.eventFirstTime:` 指出這是否為第一次為此視訊呼叫此媒體事件； </li><li> `media.mediaEvent:` 包含造成監控呼叫的事件名稱的字串。 </li></ul> |
|  | `media.mediaEvent` events： <ul><li> `OPEN:` 透過 `Media.autoTrack` 或對 `Media.play` 呼叫第一次觀察到播放時； </li><li> `CLOSE:` 當播放透過 `Media.autoTrack` 或對 `Media.close` 的呼叫在完成視訊結束時；</li><li> `PLAY:` 當播放在暫停或擦除之後，透過 `Media.autoTrack` 或對 `Media.play` 的第二個呼叫繼續；</li><li> `STOP:` 當播放由於透過 `Media.autoTrack` 或對 `Media.stop` 呼叫的擦除開始的暫停而停止時；</li><li> `MONITOR:` 我們的自動監視在播放視訊時檢查視訊的狀態時 (每秒)；</li><li> `SECONDS:` 以 `Media.trackSeconds` 變數定義的秒數間隔；</li><li> `MILESTONE:` 在 `Media.trackMilestones` 變數定義的里程碑； </li></ul> |
| `Media.track` | **語法：** <br/><br/> `s.Media.track(mediaName)`<br/><br/>立即傳送目前的視訊狀態，以及您定義的任何 `Media.trackVars` 和 Media.trackEvents。此方法是在 `Media.monitor` 內使用。<br/><br/>請參閱[使用 Media.monitor 測量其他度量。](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) <br/><br/>在呼叫此方法之前，在視訊上呼叫 `Media.open` 和 `Media.play`。此方法會採用下列參數： <ul> <li> **mediaName**：視訊的名稱。這必須符合 `Media.open` 中使用的名稱。</li> </ul> 此方法是在播放視訊時傳送其他變數的唯一方式。此方法會將秒數間隔和百分比里程碑計數器重設為零，以避免多個追蹤點擊。 |


## 追蹤視訊播放器事件 {#track-video-player-events}

您可以透過建立附加至視訊播放器事件處理常式的函式來追蹤媒體播放器.這可讓您在適當時機呼叫 `Media.open`、`Media.play`、`Media.stop` 和 `Media.close`。例如：

* **載入：**&#x200B;呼叫 `Media.open` 和 `Media.play`
* **暫停：**&#x200B;呼叫 `Media.stop`。例如，使用者若在 15 秒後暫停視訊，則呼叫 `s.Media.stop("Video1", 15)`
* **緩衝：**&#x200B;當視訊緩衝時呼叫 `Media.stop`。當繼續播放時呼叫 `Media.play`。
* **繼續：**&#x200B;呼叫 `Media.play`。例如，使用者若在起始播放視訊 15 秒後繼續播放視訊，則呼叫 `s.Media.play("Video1", 15)`。
* **Scrub (滑桿)：**&#x200B;當使用者拖曳視訊滑桿時，呼叫 `Media.stop`。當使用者放開視訊滑桿時，呼叫 `Media.play`。
* **結束：**&#x200B;呼叫 `Media.stop`，然後呼叫 `Media.close`。例如，在長 100 秒的視訊結束時，呼叫 `s.Media.stop("Video1", 100)`，然後呼叫 `s.Media.close("Video1")`。

若要完成此操作，可以定義能夠從媒體播放器事件處理常式呼叫的四個自訂函數。傳入 `Media.open`、`Media.play`、`Media.stop` 和 `Media.close` 的各種參數皆來自播放器。下列偽代碼說明如何進行操作：

```javascript
/* Call on video load */
function startMovie() {
    s.Media.open(mediaName, mediaLength, mediaPlayerName);
    playMovie();
}

/* Call on video resume from pause and slider release */
function playMovie() {
    s.Media.play(mediaName,
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength);
}
/* Call on video pause and slider grab */
function stopMovie() {
    s.Media.stop(mediaName, mediaOffset);
}

/* Call on video end */
/* Measuring Video for Developers 43 */
function endMovie() {
    stopMovie();
    s.Media.close(mediaName);
}
```

## JavaScript 自動追蹤 {#javascript-autotrack}

JavaScript 媒體模組會識別頁面 HTML 中的所有 `<embed>` 或 `<object>` 標記。然後它會搜尋每個標記中的資料，以決定要使用的媒體播放器 (如果有的話)。如果播放器為 Windows Media Player、Quicktime 或 Real Player，則可以使用 `autoTrack`，不過 Windows Media Player 適用的 僅能對 Internet Explorer 運作。`autoTrack`需要手動追蹤 Windows Media Player，才能支援所有其他瀏覽器。

您必須在要追蹤的物件上設定 `classid` 屬性。需要 `classid`，才能公開媒體模組使用的事件處理常式，以自動追蹤視訊。

```javascript
s.Media.autoTrack = true
```

## JavaScript 程式碼範例 {#javascript-sample-code}

```javascript
// Sample implementation
s.usePlugins=true
function s_doPlugins(s) {
    /* Add manual calls to modules and plugins here */
}

s.doPlugins=s_doPlugins

/*********Media Module Calls**************/
s.loadModule("Media")

/*Configure Media Module Functions */
s.Media.autoTrack= true;
s.Media.trackVars="events, prop2, eVar1, eVar2, eVar3";
s.Media.trackEvents="event1, event2, event3, event4, event5, event6, event7"
s.Media.trackMilestones="25, 50, 75";
s.Media.playerName="My Media Player";
s.Media.segmentByMilestones = true;
s.Media.trackUsingContextData = true;
s.Media.contextDataMapping = {
    "a.media.name":"eVar2, prop2",
    "a.media.segment":"eVar3",
    "a.contentType":"eVar1",
    "a.media.timePlayed":"event3",
    "a.media.view":"event1",
    "a.media.segmentView":"event2",
    "a.media.complete":"event7",
    "a.media.milestones":{
        25:"event4",
        50:"event5",
        75:"event6"
    }
}

s.Media.monitor = function (s, media) { } //If Needed

/* Turn on and configure debugging here */
s.debugTracking = true;
s.trackLocal = true;

/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor
data is collected. Changes should only be made when instructed to do so by your account
manager.*/
s.visitorNamespace = "yourNamespace";
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL
s.dc = '122';

/************************** PLUGINS SECTION *************************/
/* Insert any plugins code you want to use here. */

/****************************** MODULES *****************************/
/* Insert the media module tracking code here. */
```
