---
title: 設定適用於串流媒體的 Analytics實作的第一步
description: 了解如何實作Adobe串流媒體。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 723cfab6dd2d63448f44dc535724ffe4fd0ec8a7
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 10%

---

# 使用Experience Platform邊緣安裝Media Analytics

Adobe Experience Platform Edge 可讓您將預計要送給多個產品的資料傳送到一個集中位置。 Experience Edge 會將適當的資訊轉送給所需的產品。 此概念可讓您整合實作工作，特別是橫跨多個資料解決方案時。

下圖說明使用Media Analytics Edge的Experience Platform實施：

![邊緣實作](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>目前，您只能使用Adobe Experience Platform Mobile SDK將資料傳送至Experience Edge。


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

完成下列章節，使用Experience Platform邊緣實作Media Analytics:

* [定義報表套裝](#define-a-report-suite)
* [在Adobe Experience Platform中設定結構](#set-up-the-schema-in-adobe-experience-platform)
* [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform)
* [在Adobe Experience Platform中設定資料流](#configure-a-datastream-in-adobe-experience-platform)
* [在 Customer Journey Analytics 中建立連線](#create-a-connection-in-customer-journey-analytics)
* [在Customer Journey Analytics中建立資料檢視](#create-a-data-view-in-customer-journey-analytics)
* [在Customer Journey Analytics中建立和設定專案](#create-and-configure-a-project-in-customer-journey-analytics)
* [使用Edge擴充功能將資料傳送至Experience PlatformEdge](#send-data-to-experience-platform-edge-with-the-edge-extension)

## 定義報表套裝

>[!NOTE]
>
>只有在您使用Adobe Analytics時，才需要報表套裝。 如果您打算使用Customer Journey Analytics來製作報表，則不需要報表套裝。

如果您打算使用Adobe Analytics製作報表，則需要有一個報表套裝才能與串流媒體實作搭配使用。 如需定義報表套裝的相關資訊，請參閱 [報表套裝管理器](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

定義報表套裝後，請繼續 [在Adobe Experience Platform中設定結構](#set-up-the-schema-in-adobe-experience-platform).

## 在Adobe Experience Platform中設定結構

為了標準化資料彙集以跨利用 Adobe Experience Platform 的應用程式使用，Adobe 建立了開放且公開記錄標準，即體驗資料模型 (XDM)。

要建立和設定架構，請執行以下操作：

1. 在Adobe Experience Platform中，開始建立結構，如 [在UI中建立和編輯結構](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   建立架構時，請選擇 [!UICONTROL **XDM ExperienceEvent**] 從 [!UICONTROL **建立結構**] 下拉式功能表。

1. 在 [!UICONTROL **組合物**] 區域，在 [!UICONTROL **欄位群組**] 部分，選擇 [!UICONTROL **新增**]，然後搜尋，並將下列新欄位群組新增至架構：
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   新增欄位群組後，欄位群組應會顯示在 [!UICONTROL **欄位群組**] 部分，如下所示：

   ![新增欄位群組](assets/schema-field-groups-added.png)

1. 在 [!UICONTROL **結構**] ，選擇 `endUserIds` > `_experience` 欄位群組，然後選取 [!UICONTROL **管理相關欄位**].

   ![「管理相關欄位」按鈕](assets/manage-related-fields.png)

1. 更新結構如下：

   * 在 `Adobe Analytics ExperienceEvent Template` 欄位組，隱藏除 `EndUserIDs`.

   * 在 `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` 欄位組，隱藏除「 `Identifier` 欄位。

   * 在 `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` 欄位組，隱藏除「 `Identifier` 欄位。

      ![隱藏欄位](assets/schema-hide-fields.png)

1. 選擇 [!UICONTROL **確認**] 來儲存變更。

1. 在 [!UICONTROL **結構**] ，選擇 `Implementation Details` 欄位組，選擇 [!UICONTROL **管理相關欄位**]，然後依照下列方式更新結構：

   * 在 `Implementation Details` > `Implementation details` 欄位組，隱藏除 `version`.

      ![隱藏欄位](assets/schema-hide-fields2.png)

1. 選擇 [!UICONTROL **確認**] 來儲存變更。

1. 在 [!UICONTROL **結構**] ，選擇 `Media Collection Details` 欄位組，選擇 [!UICONTROL **管理相關欄位**]，然後依照下列方式更新結構：

   * 在 `Media Collection Details` 欄位組，隱藏 `List Of States` 欄位群組。

      ![隱藏媒體收集狀態](assets/schema-hide-media-collection-states.png)

   * 在 `Media Collection Details` > `Advertising Details` 欄位群組，隱藏下列報表欄位： `Ad Completed`, `Ad Started`，和 `Ad Time Played`.

   * 在 `Media Collection Details` > `Advertising Pod Details` 欄位群組，隱藏下列報表欄位： `Ad Break ID`

   * 在 `Media Collection Details` > `Chapter Details` 欄位群組，隱藏下列報表欄位： `Chapter ID`, `Chapter Completed`, `Chapter Started`，和 `Chapter Time Played`.

   * 在 `Media Collection Details` > `Qoe Data Details` 欄位群組，隱藏下列報表欄位： `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`，和 `Total Stalling Duration`.

   * 在 `Media Collection Details` > `Session Details` 欄位群組，隱藏下列報表欄位： `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`，和 `Pccr`.

   * 在 `Media Collection Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 欄位群組，隱藏下列報表欄位： `Player State Count`, `Player State Set`，和 `Player State Time`.

      ![隱藏欄位](assets/schema-hide-listofstates.png)

1. 選擇 [!UICONTROL **確認**] 來儲存變更。

1. 在 [!UICONTROL **結構**] ，選擇 `List Of Media Collection Downloaded Content Events` 欄位組，選擇 [!UICONTROL **管理相關欄位**]，然後依照下列方式更新結構：

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` 欄位組，隱藏 `List Of States` 欄位群組。

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 欄位群組，隱藏下列報表欄位： `Ad Completed`, `Ad Started`，和 `Ad Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 欄位群組，隱藏下列報表欄位： `Ad Break ID`

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 欄位群組，隱藏下列報表欄位： `Chapter ID`, `Chapter Completed`, `Chapter Started`，和 `Chapter Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 欄位群組，隱藏下列報表欄位： `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`，和 `Total Stalling Duration`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 欄位群組，隱藏下列報表欄位： `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`，和 `Pccr`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 欄位群組，隱藏下列報表欄位： `Player State Count`, `Player State Set`，和 `Player State Time`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details`  欄位組，隱藏 `Media Session ID` 欄位。

1. 選擇 [!UICONTROL **確認**] 來儲存變更。

1. 在 [!UICONTROL **結構**] ，選擇 `Media Reporting Details` 欄位組，選擇 [!UICONTROL **管理相關欄位**]，然後依照下列方式更新結構：

   * 在 `Media Reporting Details` 欄位組，隱藏以下欄位組： `Error Details`, `List Of States End`, `List of States Start`, `Playhead`，和 `Media Session ID`.

1. 選擇 [!UICONTROL **確認**] > [!UICONTROL **儲存**]  來儲存變更。

1. 繼續 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

## 在Adobe Experience Platform中建立資料集

1. 請務必依照 [在Adobe Experience Platform中設定結構](#set-up-the-schema-in-adobe-experience-platform).

1. 在Adobe Experience Platform中，開始建立資料集，如 [資料集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hant#create).

   為資料集選取結構時，請選取您先前建立的結構，如 [在Adobe Experience Platform中設定結構](#set-up-the-schema-in-adobe-experience-platform).

1. 繼續 [在Customer Journey Analytics中設定資料流](#configure-a-datastream-in-adobe-experience-platform).

## 在Adobe Experience Platform中設定資料流

1. 請確定您已建立資料集，如 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

1. 建立新資料流，如 [設定資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hant).

   建立資料流時，請務必選取下列設定：

   * 在 [!UICONTROL **事件結構**] 欄位，確保您選取您在 [在Adobe Experience Platform中設定結構](#set-up-the-schema-in-adobe-experience-platform). 選取&#x200B;[!UICONTROL **「儲存」**]。

      >[!IMPORTANT]
          >
      >不選擇 [!UICONTROL **儲存並新增對應**] 因為這麼做會導致時間戳欄位的對應錯誤。
      

      ![建立資料流並選取結構](assets/datastream-create-schema.png)

   * 視您使用Adobe Analytics或Customer Journey Analytics而定，將下列其中一項服務新增至資料流：

      * [!UICONTROL **Adobe Analytics**] (若使用Adobe Analytics)

         如果您使用Adobe Analytics，請務必定義報表套裝，如區段所述 [定義報表套裝](#define-a-report-suite) 這篇文章。

      * [!UICONTROL **Adobe Experience Platform**] (若使用Customer Journey Analytics)
      如需如何將服務新增至資料流的詳細資訊，請參閱 [設定資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      ![新增Adobe Analytics服務](assets/datastream-add-service.png)

   * 展開 [!UICONTROL **進階選項**]，然後啟用 [!UICONTROL **Media Analytics**] 選項。

      ![Media Analytics選項](assets/datastream-media-check.png)


1. 繼續 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

## 在 Customer Journey Analytics 中建立連線

>[!NOTE]
>
>只有在您使用Customer Journey Analytics時，才需要執行下列程式。


1. 請確定您已建立資料流，如 [在Customer Journey Analytics中設定資料流](#configure-a-datastream-in-adobe-experience-platform).

1. 在Customer Journey Analytics中，建立連線，如 [建立連線](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hant).

   建立連線時，實作串流媒體需要下列設定選項：

   1. 選取您先前建立的資料集，如 [在Adobe Experience Platform中建立資料集](#create-a-dataset-in-adobe-experience-platform).

   1. 確保 [!UICONTROL **匯入所有新資料**] 設定。

1. 繼續 [在Customer Journey Analytics中建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

## 在Customer Journey Analytics中建立資料檢視

>[!NOTE]
>
>只有在您使用Customer Journey Analytics時，才需要執行下列程式。

1. 請確定您已在Customer Journey Analytics中建立連線，如 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

1. 在Customer Journey Analytics中，建立資料檢視，如 [建立或編輯資料檢視](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hant).

   建立資料檢視時，實作串流媒體需要下列設定選取項目：

   1. 在 [!UICONTROL **連線**] 欄位中，選取您先前建立的連線，如 [在Customer Journey Analytics中建立連線](#create-a-connection-in-customer-journey-analytics).

      您建立的連線最多可能需要15分鐘才能供選取。

   1. 在 [!UICONTROL **元件**] 標籤中 [!UICONTROL **結構欄位**] 區段，搜尋下表中列出的每個元件，並將其拖曳至 [!UICONTROL **量度**] 中。 如果有多個相同名稱的欄位，請使用XDM路徑，確保是正確的欄位。

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
      | 章節開始 | mediaReporting.chapterDetails.isStarted |
      | 章節完成 | mediaReporting.chapterDetails.isCompleted |
      | 章節播放時間 | mediaReporting.chapterDetails.timePlayed |
      | 廣告開始 | mediaReporting.advertisingDetails.isStarted |
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
      | 播放器狀態集 | mediaReporting.states.isSet |
      | 播放器狀態計數 | mediaReporting.states.count |
      | 播放器狀態時間 | mediaReporting.states.time |


   1. 更新標籤(在 [!UICONTROL **內容標籤**] 下拉式選單)（適用於下表中的元件）。 搜尋量度面板中未包含的任何元件，並將其拖曳至面板。

      | 元件名稱 | 內容標籤 |
      |---------|----------|
      | 媒體工作階段伺服器逾時 | 媒體：上次呼叫後秒數 |
      | 媒體逗留時間 | 媒體：媒體逗留時間 |
      | 總緩衝期間 | 媒體：總緩衝期間 |
      | 開始時間 | 媒體：開始時間 |
      | 總暫停期間 | 媒體：總暫停期間 |

   1. 若要將劃分加入您的Customer Journey Analytics專案，請將下列維度加入 [!UICONTROL **Dimension**] 面板：

      | XDM路徑 | 元件名稱 |
      |---------|----------|
      | mediaReporting.states.name | 播放器狀態名稱 |
      | mediaReporting.sessionDetails.ID | 媒體工作階段 ID |

      除了此表格中的維度，您也可以新增至任何其他維度，讓您可用於篩選Customer Journey Analytics專案中的資料。

1. 選擇 [!UICONTROL **保存並繼續**] > [!UICONTROL **保存並完成**] 來儲存變更。

1. 繼續 [在Customer Journey Analytics中建立和設定專案](#create-and-configure-a-project-in-customer-journey-analytics).

## 在Customer Journey Analytics中建立和設定專案

1. 請確定您已按照以下說明以Customer Journey Analytics建立資料檢視： [在Customer Journey Analytics中建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

1. 在Customer Journey Analytics中，在 [!UICONTROL **工作區**] 標籤中 [!UICONTROL **專案**] 區域，選擇 [!UICONTROL **建立專案**].

1. 選擇 [!UICONTROL **空白專案**] > [!UICONTROL **建立**].

1. 在新專案中，選取您先前建立的資料檢視。

   在專案中建立面板時，您可以使用新增至資料檢視的任何元件，如 [在Customer Journey Analytics中建立資料檢視](#create-a-new-data-view-in-customer-journey-analytics).

   以下4個面板是您可建立的面板範例：

   ![主要內容面板](assets/main-content-panel.png)

   ![章節和廣告面板](assets/chapter-and-ads-panel.png)

   ![QoE面板](assets/qoe-panel.png)

   ![播放器狀態面板](assets/player-state-panel.png)

1. 選取 **面板** 圖示，然後拖曳 [!UICONTROL **媒體同時檢閱者**] 面板和 [!UICONTROL **媒體播放逗留時間**] 中。

   2個面板應如下所示：

   ![媒體同時檢閱者面板](assets/media-concurrent-viewers-panels.png)

   ![媒體播放逗留時間面板](assets/media-playback-time-spent-panels.png)

1. 依照 [共用專案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   如果您要共用的使用者無法使用，請確定使用者擁有Adobe Admin Console中Customer Journey Analytics的使用者和管理員存取權。

1. 繼續 [傳送資料至Experience PlatformEdge](#send-data-to-experience-platform-edge).

## 使用AEP Mobile SDK將資料傳送至Experience PlatformEdge

您可以使用Adobe Experience Platform行動SDK將行動資料傳送至Experience Platform Edge。 (或者，您也可以使用Edge API的自訂實作。<!-- I guess we don't need/want to document this? -->)

使用下列檔案資源來完成實作：


| 行動作業系統 | 資源 |
|---------|----------|
| **iOS 應用程式** | 下列資源可用於傳送iOS行動資料： <ul><li>[使用資料收集UI設定行動SDK](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/getting-started.md)</li><li>[從Media SDK移轉至Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API參考](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/api-reference.md)</li></ul> |
| **Android** | 下列資源可用於傳送Android行動資料： <ul><li>[使用資料收集UI設定行動SDK](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/getting-started.md)</li><li>[從Media SDK移轉至Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API參考](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/api-reference.md)</li></ul> |


<!--

+++Adobe Experience Platform Mobile SDK

If you plan to use the Mobile SDK extension in Adobe Experience Platform Data Collection to send data to Edge, complete the following sections:

### Create a mobile property

Create a mobile property, as described in [Set up a mobile property](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/). 

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/mobile-sdk/overview.html?lang=en 

The Adobe Experience Platform Mobile SDK helps power Adobe's Experience Cloud solutions and services in your mobile apps. It is available for Android, iOS, and various cross-platform development frameworks. Configuration is handled through Adobe Experience Platform Data Collection.
>[!IMPORTANT]
>
>An Adobe Analytics extension is also available in Adobe Experience Platform Data Collection. If you install this extension, you do not take advantage of XDM or the Edge Network.

### Register the extensions and load your tag configuration

Use code in your app to register the necessary extensions and load your tag configuration. For more information, see [Set up the configuration](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Implement and test fuctionality

Implement and test app functionality using a combination of tags data elements, rules, additional extensions, and SDK API calls. Inspect, validate, and debug data collection and experiences for your mobile application.

For more information, see [Use the sample application](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Extend and validate your mobile app implementation

Before pushing the mobile app extension to your production environment, first validate that it works.

(What are the steps to do this?)

-->

<!--

+++Adobe Experience Platform Web SDK (Coming soon)

>[!NOTE]
>
>The Adobe Experience Platform Web SDK is not yet available. This page will be updated when it becomes available.

<!-- Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/web-sdk/overview.html?lang=en -->

<!-- Use the Web SDK extension in Adobe Experience Platform Data Collection to send data to Edge.

You can use the [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html) to send data to Adobe Analytics. This implementation method works by translating the [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) into a format used by Analytics.

You can send data to Experience Edge directly using the Web SDK, or through the Web SDK extension in Tags. -->

<!-- ### Web SDK

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK workflow](../../assets/websdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td> 4</td>
<td><b>Install the prebuilt standalone version</b>. You can reference the library (<code>alloy.js</code>) on the CDN directly on your page or download and host it on your own infrastructure. Alternatively, you can use the NPM package.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-2%3A-installing-the-prebuilt-standalone-version">Installing the prebuilt standalone version</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-3%3A-using-the-npm-package">Using the NPM package</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>6</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>7</td>
<td><b>Configure the Web SDK</b>. Ensure the library that you installed in step 4 is properly configured with the datastream ID (formerly known as edge configuration id (<code>edgeConfigId</code>)), organization id (<code>orgId</code>), and other available options.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en">Configure the Web SDK</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Execute commands</b> and/or <b>track events</b>. After the base code has been implemented on your webpage, you can begin executing commands and tracking events with the SDK.
</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/executing-commands.html?lang=en">Execute commands</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en">Track events</a></td>
</tr>

<tr>
<td>9</td><td><b>Extend and validate your implementation</b> before pushing it out to production.</td><td></td> 
</tr>
</table>


### Web SDK extension

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK extension workflow](../../assets/websdk-extension-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td>4</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<tr>
<td>5</td> 
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>6</td>
<td><b>Create a tag property</b>. Properties are overarching containers used to reference tag management data.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#for-web">Create or configure a tag property for web</a></td>
</tr>

<tr>
<td>7</td> 
<td><b>Install and configure the Web SDK extension</b> in your tag property. Configure the Web SDK extension to send data to the datastream configured in step 4.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html?lang=en">Adobe Experience Platform Web SDK extension overview</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Iterate, validate, and publish</b> to production. Add the tag property to your web site. Then use data elements, rules, and so on, to customize your implementation.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=en">Publishing overview</a></td>
</tr>

</table>


### Additional resources

Tags can be highly customized. Learn more about how you can get the most out of Adobe Analytics by including the right data in your implementation.

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#): Learn how the interface works and what extensions are available.

-   [Adobe Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/web-sdk.html?lang=en)


+++

-->


<!--

### Adobe Experience Platform SDK

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>4</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Create a mobile property</b>. A property is a container that you fill with extensions, rules, data elements, and libraries.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/">Set up a mobile property</a></tr>

<tr>
<td>6</td>
<td><b>Install the Adobe Experience Platform Edge Network extension</b> in the mobile tag property and configure the datastream in the extension.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/edge-network/">Adobe Experience Platform Edge Network</a>
</tr>

<tr>
<td>7</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>9</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>


### Adobe Analytics extension.

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-analytics-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Install the Adobe Analytics extension</b> in the mobile tag property and configure the extension to point to your report suite.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/adobe-analytics/">Adobe Analytics extension for mobile property</a>
</tr>

<tr>
<td>4</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>6</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>

### Additional resources

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#)

-   [Mobile SDK documentation](https://developer.adobe.com/client-sdks/documentation/)

-->

<!--

+++

+++Edge Network Server API

Send data directly to Edge using an API.

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/edge-api/overview.html?lang=en 

If you are unable to use the Adobe Experience Platform [Web SDK](../web-sdk/overview.md) or [Mobile SDK](../mobile-sdk/overview.md), you can send data to the Edge Network directly through an API.

See [Edge Network Server API documentation](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html), and an example [integrating with Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/interacting-other-adobe-solutions/interacting-adobe-analytics.html).

+++ 

-->

