---
title: 設定適用於流媒體的 Analytics實作的首要步驟
description: 瞭解如何實作Adobe串流媒體。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 29d58b41-9a49-4b71-bdc5-4e2848cd3236
source-git-commit: 1280c0851094234b308e69ba2be3da21dfdc1302
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 10%

---

# 安裝Media Analytics與Experience Platform Edge

Adobe Experience Platform Edge 可讓您將預計要送給多個產品的資料傳送到一個集中位置。 Experience Edge 會將適當的資訊轉送給所需的產品。 此概念可讓您整合實作工作，特別是橫跨多個資料解決方案時。

下圖說明使用Experience Platform邊緣的Media Analytics實作：

![Edge實施](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>目前，您只能使用Adobe Experience Platform Mobile SDK傳送資料給Experience Edge。


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

完成下列章節，以使用Experience Platform Edge實作Media Analytics：

* [定義報表套裝](#define-a-report-suite)
* [在Adobe Experience Platform中設定結構描述](#set-up-the-schema-in-adobe-experience-platform)
* [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform)
* [在Adobe Experience Platform中設定資料串流](#configure-a-datastream-in-adobe-experience-platform)
* [在 Customer Journey Analytics 中建立連線](#create-a-connection-in-customer-journey-analytics)
* [以Customer Journey Analytics建立資料檢視](#create-a-data-view-in-customer-journey-analytics)
* [在Customer Journey Analytics中建立及設定專案](#create-and-configure-a-project-in-customer-journey-analytics)
* [使用Edge擴充功能傳送資料給Experience Platform Edge](#send-data-to-experience-platform-edge-with-the-edge-extension)

## 定義報表套裝

>[!NOTE]
>
>只有當您使用Adobe Analytics時，才需要報表套裝。 如果您打算使用Customer Journey Analytics來製作報表，則不需要報表套裝。

如果您打算使用Adobe Analytics製作報表，則需要有可搭配串流媒體實作使用的報表套裝。 如需定義報表套裝的相關資訊，請參閱 [報表套裝管理員](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

定義報表套裝後，繼續使用 [在Adobe Experience Platform中設定結構描述](#set-up-the-schema-in-adobe-experience-platform).

## 在Adobe Experience Platform中設定結構描述

為了標準化資料彙集以跨利用 Adobe Experience Platform 的應用程式使用，Adobe 建立了開放且公開記錄標準，即體驗資料模型 (XDM)。

若要建立及設定綱要：

1. 在Adobe Experience Platform中，依照中的說明開始建立結構描述 [在UI中建立和編輯結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   建立結構描述時，請選擇 [!UICONTROL **XDM ExperienceEvent**] 從 [!UICONTROL **建立結構描述**] 下拉式功能表。

1. 在 [!UICONTROL **組合**] 區域，在 [!UICONTROL **欄位群組**] 區段，選取 [!UICONTROL **新增**]，然後搜尋下列新欄位群組並將其新增至結構描述：
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   新增欄位群組後，這些群組應會顯示在 [!UICONTROL **欄位群組**] 區段，如下所示：

   ![已新增欄位群組](assets/schema-field-groups-added.png)

1. 在 [!UICONTROL **結構**] 區域，選取 `endUserIds` > `_experience` 欄位群組，然後選取 [!UICONTROL **管理相關欄位**].

   ![管理相關欄位按鈕](assets/manage-related-fields.png)

1. 更新結構，如下所示：

   * 在 `Adobe Analytics ExperienceEvent Template` 欄位群組，隱藏所有欄位，但 `EndUserIDs`.

   * 在 `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` 欄位群組，隱藏所有欄位 `Identifier` 欄位。

   * 在 `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` 欄位群組，隱藏所有欄位 `Identifier` 欄位。

     ![要隱藏的欄位](assets/schema-hide-fields.png)

1. 選取 [!UICONTROL **確認**] 以儲存變更。

1. 在 [!UICONTROL **結構**] 區域，選取 `Implementation Details` 欄位群組，選取 [!UICONTROL **管理相關欄位**]，然後更新結構，如下所示：

   * 在 `Implementation Details` > `Implementation details` 欄位群組，隱藏所有欄位，但 `version`.

     ![要隱藏的欄位](assets/schema-hide-fields2.png)

1. 選取 [!UICONTROL **確認**] 以儲存變更。

1. 在 [!UICONTROL **結構**] 區域，選取 `Media Collection Details` 欄位群組，選取 [!UICONTROL **管理相關欄位**]，然後更新結構，如下所示：

   * 在 `Media Collection Details` 欄位群組，隱藏 `List Of States` 欄位群組。

     ![隱藏媒體收集狀態](assets/schema-hide-media-collection-states.png)

   * 在 `Media Collection Details` > `Advertising Details` 欄位群組，隱藏下列報表欄位： `Ad Completed`， `Ad Started`、和 `Ad Time Played`.

   * 在 `Media Collection Details` > `Advertising Pod Details` 欄位群組，隱藏下列報表欄位： `Ad Break ID`

   * 在 `Media Collection Details` > `Chapter Details` 欄位群組，隱藏下列報表欄位： `Chapter ID`， `Chapter Completed`， `Chapter Started`、和 `Chapter Time Played`.

   * 在 `Media Collection Details` > `Qoe Data Details` 欄位群組，隱藏下列報表欄位： `Average Bitrate`， `Average Bitrate Bucket`， `Bitrate Changes`， `Buffer Events`， `Total Buffer Duration`， `Errors`， `External Error IDs`， `Bitrate Change Impacted Streams`， `Buffer Impacted Streams`， `Dropped Frame Impacted Streams`， `Error Impacted Streams`， `Stalling Impacted Streams`， `Drops Before Starts`， `Media SDK Error IDs`， `Player SDK Error IDs`， `Stalling Events`、和 `Total Stalling Duration`.

   * 在 `Media Collection Details` > `Session Details` 欄位群組，隱藏下列報表欄位： `Media Session ID`， `Ad Count`， `Average Minute Audience`， `Chapter Count`， `Estimated Streams`， `Pause Impacted Streams`， `10% Progress Marker`， `25% Progress Marker`， `50% Progress Marker`， `75% Progress Marker`， `95% Progress Marker`， `Media Segment Views`， `Content Completes`， `Media Downloaded Flag`， `Federated Data`， `Content Starts`， `Media Starts`， `Pause Events`， `Total Pause Duration`， `Media Session Server Timeout`， `Video Segment`， `Content Time Spent`， `Media Time Spent`， `Unique Time Played`， `Pev3`、和 `Pccr`.

   * 在 `Media Collection Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 欄位群組，隱藏下列報表欄位： `Player State Count`， `Player State Set`、和 `Player State Time`.

     ![要隱藏的欄位](assets/schema-hide-listofstates.png)

1. 選取 [!UICONTROL **確認**] 以儲存變更。

1. 在 [!UICONTROL **結構**] 區域，選取 `List Of Media Collection Downloaded Content Events` 欄位群組，選取 [!UICONTROL **管理相關欄位**]，然後更新結構，如下所示：

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` 欄位群組，隱藏 `List Of States` 欄位群組。

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 欄位群組，隱藏下列報表欄位： `Ad Completed`， `Ad Started`、和 `Ad Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 欄位群組，隱藏下列報表欄位： `Ad Break ID`

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 欄位群組，隱藏下列報表欄位： `Chapter ID`， `Chapter Completed`， `Chapter Started`、和 `Chapter Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 欄位群組，隱藏下列報表欄位： `Average Bitrate`， `Average Bitrate Bucket`， `Bitrate Changes`， `Buffer Events`， `Total Buffer Duration`， `Errors`， `External Error IDs`， `Bitrate Change Impacted Streams`， `Buffer Impacted Streams`， `Dropped Frame Impacted Streams`， `Error Impacted Streams`， `Stalling Impacted Streams`， `Drops Before Starts`， `Media SDK Error IDs`， `Player SDK Error IDs`， `Stalling Events`、和 `Total Stalling Duration`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 欄位群組，隱藏下列報表欄位： `Media Session ID`， `Ad Count`， `Average Minute Audience`， `Chapter Count`， `Estimated Streams`， `Pause Impacted Streams`， `10% Progress Marker`， `25% Progress Marker`， `50% Progress Marker`， `75% Progress Marker`， `95% Progress Marker`， `Media Segment Views`， `Content Completes`， `Media Downloaded Flag`， `Federated Data`， `Content Starts`， `Media Starts`， `Pause Events`， `Total Pause Duration`， `Media Session Server Timeout`， `Video Segment`， `Content Time Spent`， `Media Time Spent`， `Unique Time Played`， `Pev3`、和 `Pccr`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 欄位群組，隱藏下列報表欄位： `Player State Count`， `Player State Set`、和 `Player State Time`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details`  欄位群組，隱藏 `Media Session ID` 欄位。

1. 選取 [!UICONTROL **確認**] 以儲存變更。

1. 在 [!UICONTROL **結構**] 區域，選取 `Media Reporting Details` 欄位群組，選取 [!UICONTROL **管理相關欄位**]，然後更新結構，如下所示：

   * 在 `Media Reporting Details` 欄位群組，隱藏下列欄位群組： `Error Details`， `List Of States End`， `List of States Start`， `Playhead`、和 `Media Session ID`.

1. 選取 [!UICONTROL **確認**] > [!UICONTROL **儲存**]  以儲存變更。

1. 繼續使用 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

## 在Adobe Experience Platform中建立資料集

1. 請確定您設定了結構描述，如所述 [在Adobe Experience Platform中設定結構描述](#set-up-the-schema-in-adobe-experience-platform).

1. 在Adobe Experience Platform中，依照中的說明開始建立資料集 [資料集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hant#create).

   為資料集選取結構描述時，請選擇您先前建立的結構描述，如中所述 [在Adobe Experience Platform中設定結構描述](#set-up-the-schema-in-adobe-experience-platform).

1. 繼續使用 [在Customer Journey Analytics中設定資料串流](#configure-a-datastream-in-adobe-experience-platform).

## 在Adobe Experience Platform中設定資料串流

1. 請確定您已建立資料集，如所述 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

1. 建立新的資料串流，如所述 [設定資料串流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hant).

   建立資料串流時，請務必進行下列設定選擇：

   * 在 [!UICONTROL **事件結構描述**] 欄位建立資料流時，請確定您選取之前在中建立的結構描述 [在Adobe Experience Platform中設定結構描述](#set-up-the-schema-in-adobe-experience-platform). 選取&#x200B;[!UICONTROL **「儲存」**]。

     >[!IMPORTANT]
     >
         >不要選取 [!UICONTROL **儲存並新增對應**] 因為這樣做會導致「時間戳記」欄位的對應錯誤。
     
     ![建立資料流並選取結構描述](assets/datastream-create-schema.png)

   * 根據您使用的是Adobe Analytics還是Customer Journey Analytics，將以下任一服務新增至資料流：

      * [!UICONTROL **Adobe Analytics**] (若使用Adobe Analytics)

        如果您使用Adobe Analytics，請務必定義報表套裝，如區段所述 [定義報表套裝](#define-a-report-suite) 本文章內容。

      * [!UICONTROL **Adobe Experience Platform**] (若使用Customer Journey Analytics)

     如需如何將服務新增至資料流的詳細資訊，請參閱以下主題中的「將服務新增至資料流」一節： [設定資料串流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![新增Adobe Analytics服務](assets/datastream-add-service.png)

   * 展開 [!UICONTROL **進階選項**]，然後啟用 [!UICONTROL **媒體分析**] 選項。

     ![媒體分析選項](assets/datastream-media-check.png)

1. 繼續使用 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

## 在 Customer Journey Analytics 中建立連線

>[!NOTE]
>
>只有在使用Customer Journey Analytics時，才需要執行下列程式。


1. 請確定您已建立資料串流，如所述 [在Customer Journey Analytics中設定資料串流](#configure-a-datastream-in-adobe-experience-platform).

1. 在Customer Journey Analytics中建立連線，如所述 [建立連線](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hant).

   建立連線時，實作串流媒體需要下列設定選項：

   1. 選取您先前建立的資料集，如所述 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

   1. 確保 [!UICONTROL **匯入所有新資料**] 設定已啟用。

1. 繼續使用 [以Customer Journey Analytics建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

## 以Customer Journey Analytics建立資料檢視

>[!NOTE]
>
>只有在使用Customer Journey Analytics時，才需要執行下列程式。

1. 請確定您已在Customer Journey Analytics中建立連線，如所述 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

1. 在Customer Journey Analytics中，建立資料檢視，如所述 [建立或編輯資料檢視](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hant).

   建立資料檢視時，實作串流媒體需要以下設定選項：

   1. 在 [!UICONTROL **連線**] 欄位中，選取您先前建立的連線，如所述 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

      您建立的連線最多可能需要15分鐘才能選取。

   1. 於 [!UICONTROL **元件**] 標籤，在 [!UICONTROL **結構描述欄位**] 區段，搜尋下表中列出的每個元件，並將其拖曳至 [!UICONTROL **量度**] 面板。 如果存在多個相同名稱的欄位，請使用XDM路徑來確保它是正確的欄位。

      **主要內容 — 內容量度**

      | 元件名稱 | XDM路徑 |
      |----------|---------|
      | 媒體開始次數 | mediaReporting.sessionDetails.isViewed |
      | 媒體區段檢視次數 | mediaReporting.sessionDetails.hasSegmentView |
      | 內容開始 | mediaReporting.sessionDetails.isPlayed |
      | 內容完成 | mediaReporting.sessionDetails.isCompleted |
      | 內容逗留時間 | mediaReporting.sessionDetails.timePlayed |
      | 媒體逗留時間 | mediaReporting.sessionDetails.totalTimePlayed |
      | 不重複播放時間 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10% 進度標記 | mediaReporting.sessionDetails.hasProgress10 |
      | 平均每分鐘對象數 | mediaReporting.sessionDetails.averageMinuteAudience |


      **章節與廣告 — 章節與廣告量度**

      | 元件名稱 | XDM路徑 |
      |----------|---------|
      | 章節已開始 | mediaReporting.chapterDetails.isStarted |
      | 章節已完成 | mediaReporting.chapterDetails.isCompleted |
      | 章節時間已播放 | mediaReporting.chapterDetails.timePlayed |
      | 廣告已開始 | mediaReporting.advertisingDetails.isStarted |
      | 廣告完成 | mediaReporting.advertisingDetails.isCompleted |
      | 廣告播放時間 | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE量度**

      | 元件名稱 | XDM路徑 |
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

      | 元件名稱 | XDM路徑 |
      |----------|---------|
      | 播放器狀態設定 | mediaReporting.states.isSet |
      | 播放器狀態計數 | mediaReporting.states.count |
      | 播放器狀態時間 | mediaReporting.states.time |


   1. 更新標籤(在 [!UICONTROL **內容標籤**] 下拉式功能表)。 搜尋並拖曳量度面板中尚未的任何元件至面板。

      | 元件名稱 | 內容標籤 |
      |---------|----------|
      | 媒體工作階段伺服器逾時 | 媒體：自上次呼叫以來的秒數 |
      | 媒體逗留時間 | 媒體：媒體逗留時間 |
      | 總緩衝期間 | 媒體：總緩衝期間 |
      | 開始時間 | 媒體：開始時間 |
      | 總暫停期間 | 媒體：總暫停期間 |

   1. 若要在Customer Journey Analytics專案中新增劃分，請將下列維度新增至 [!UICONTROL **Dimension**] 面板：

      | XDM路徑 | 元件名稱 |
      |---------|----------|
      | mediaReporting.states.name | 播放器狀態名稱 |
      | mediaReporting.sessionDetails.ID | 媒體工作階段 ID |

      除了此表格中的維度外，您也可以新增任何其他維度，以便在Customer Journey Analytics專案中篩選資料。

1. 選取 [!UICONTROL **儲存並繼續**] > [!UICONTROL **儲存並完成**] 以儲存變更。

1. 繼續使用 [在Customer Journey Analytics中建立及設定專案](#create-and-configure-a-project-in-customer-journey-analytics).

## 在Customer Journey Analytics中建立及設定專案

1. 請確定您已依照「 」中的說明以Customer Journey Analytics建立資料檢視 [以Customer Journey Analytics建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

1. 在Customer Journey Analytics中、在 [!UICONTROL **Workspace**] 標籤，在 [!UICONTROL **專案**] 區域，選取 [!UICONTROL **建立專案**].

1. 選取 [!UICONTROL **空白專案**] > [!UICONTROL **建立**].

1. 在新專案中，選取您先前建立的資料檢視。

   在專案中建立面板時，您可以使用新增至資料檢視的任何元件，如中所述 [以Customer Journey Analytics建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

   以下4個面板是您可以建立的面板範例：

   ![主要內容面板](assets/main-content-panel.png)

   ![章節和廣告面板](assets/chapter-and-ads-panel.png)

   ![QoE面板](assets/qoe-panel.png)

   ![平板狀態面板](assets/player-state-panel.png)

1. 選取 **面板** 圖示拖曳至「 」，接著將「 」 [!UICONTROL **媒體同時檢閱者**] 面板和 [!UICONTROL **媒體播放時間**] 面板。

   這兩個面板看起來應該像這樣：

   ![媒體同時檢閱者面板](assets/media-concurrent-viewers-panels.png)

   ![「媒體播放時間」面板](assets/media-playback-time-spent-panels.png)

1. 共用專案，如所述 [共用專案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   如果您要共用的使用者無法使用，請確認該使用者是否擁有Adobe Admin ConsoleCustomer Journey Analytics的使用者和管理員存取權。

1. 繼續使用 [傳送資料給Experience Platform Edge](#send-data-to-experience-platform-edge).

## 使用AEP Mobile SDK傳送資料給Experience Platform Edge

您可以使用Adobe Experience Platform mobile SDK將行動資料傳送至Experience Platform Edge。

使用下列檔案資源完成iOS和Android的實作：

* [快速入門](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API 參考資料](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [移轉至Adobe Streaming Media for Edge Network擴充功能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)


或者，您也可以使用下列資源來使用Edge API的自訂實作：

* [Media Edge API總覽](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Media Edge API快速入門](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Media Edge API疑難排解指南](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [使用Media Edge API的Open API規格檔案](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)