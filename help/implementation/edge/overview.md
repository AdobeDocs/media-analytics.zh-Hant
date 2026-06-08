---
title: Edge實作概觀
description: 設定透過Edge Network收集串流媒體資料所需的Adobe Experience Platform結構、資料集和資料流。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 4%

---

# Edge實作概觀

Adobe Experience Platform Edge Network可讓您將預計要用於多個產品的資料傳送至單一端點，接著將適當的資訊轉送至每個產品。 這是實作串流媒體收集的建議方法，也是從單一實作同時支援Adobe Analytics和Customer Journey Analytics的唯一方法。

舊版Media SDK方法需要每個Adobe解決方案使用產品專屬的檢測工具，相比之下，Edge實作則使用共用XDM資料模型和單一資料流。 資料會從SDK或API傳輸至Edge Network，接著路由至資料串流中設定的Adobe產品（Analytics、CJA、AJO或RTCDP）。 這表示稍後切換或新增下游產品不需要重新檢測您的媒體事件。

無論您使用哪個程式碼基底，都必須先完成本頁所述的平台設定：建立結構、建立資料集及設定資料流。

## 先決條件

1. **完成一般必要條件。** 請參閱[一般必要條件](/help/getting-started/prereqs.md)。

1. **確認相容的Adobe解決方案。** 您必須具備下列其中至少一個的有效實作：
   * [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hant)： Edge媒體資料的主要報表目的地
   * [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)：透過相同資料流支援隨附或替代CJA
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant)或[Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)：在設定其中一項時，將&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;服務新增至您的資料流

## 在Adobe Experience Platform中設定結構

為了標準化使用Adobe Experience Platform之應用程式的資料收集，Adobe建立了開放式、公開記錄的體驗資料模型(XDM)標準。

1. 在Adobe Experience Platform中，開始建立結構描述，如[在UI中建立和編輯結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)中所述。

1. 在[結構描述詳細資料]頁面上，選擇&#x200B;**[!UICONTROL 體驗事件]**&#x200B;作為結構描述的基底類別。

   ![已新增欄位群組](assets/schema-experience-event.png)

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. 指定結構描述顯示名稱和說明，然後選取&#x200B;**[!UICONTROL 完成]**。

1. 在&#x200B;**[!UICONTROL 構成]**&#x200B;區域中，在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**，然後搜尋下列欄位群組並將其新增至結構描述：
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   新增欄位群組後，它們會顯示在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段中：

   ![已新增欄位群組](assets/schema-field-groups-added.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的變更。

1. （選用）您可以在結構描述UI中隱藏某些欄位。 這些欄位是Adobe填充在後端的伺服器計算報表欄位 — 並非由SDK或API傳送，不會影響資料收集。 隱藏這些功能不會影響功能，只會減少在AEP UI中瀏覽結構描述時的視覺雜訊。 這些欄位僅參考`MediaAnalytics Interaction Details`欄位群組中的欄位。

   +++ 展開以檢視可隱藏欄位的指示。

   1. 在&#x200B;**[!UICONTROL 結構]**&#x200B;區域中，選取`Media Collection Details`欄位，然後選取&#x200B;**[!UICONTROL 管理相關欄位]**。

      ![管理相關欄位](assets/manage-related-fields.png)

   1. 啟用選項&#x200B;**[!UICONTROL 顯示欄位]**&#x200B;的顯示名稱，然後更新結構描述，如下所示：

      * 在`Media Collection Details` > `Advertising Details`欄位中，隱藏下列報告欄位： `Ad Completed`、`Ad Started`和`Ad Time Played`。

      * 在`Media Collection Details` > `Advertising Pod Details`欄位中，隱藏下列報告欄位： `Ad Break ID`

      * 在`Media Collection Details` > `Chapter Details`欄位中，隱藏下列報告欄位： `Chapter Completed`、`Chapter ID`、`Chapter Started`和`Chapter Time Played`。

      * 在`Media Collection Details`欄位中，隱藏`List Of States`欄位。

        ![隱藏媒體集合狀態](assets/schema-hide-media-collection-states.png)

      * 在`Media Collection Details` > `List Of States End`和`Media Collection Details` > `List Of States Start`欄位中，隱藏下列報告欄位： `Player State Count`、`Player State Set`和`Player State Time`。

        要隱藏的![欄位](assets/schema-hide-listofstates.png)

      * 在`Media Collection Details` > `Qoe Data Details`欄位中，隱藏下列報告欄位： `Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Impacted Streams`、`Buffer Events`、`Dropped Frame Impacted Streams`、`Drops Before Starts`、`Errors`、`External Error IDs`、`Error Impacted Streams`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Impacted Streams`、`Stalling Events`、`Total Buffer Duration`和`Total Stalling Duration`。

      * 在`Media Collection Details` > `Session Details`欄位中，隱藏下列報告欄位： `10% Progress Marker`、`25% Progress Marker`、`50% Progress Marker`、`75% Progress Marker`、`95% Progress Marker`、`Ad Count`、`Average Minute Audience`、`Content Completes`、`Chapter Count`、`Content Starts`、`Content Time Spent`、`Estimated Streams`、`Federated Data`、`Media Segment Views`、`Media Downloaded Flag`、`Media Starts`、`Media Session ID`、`Media Session Server Timeout`、`Media Time Spent`、`Pause Events`、`Pause Impacted Streams`、`Pev3`、`Pccr`、`Total Pause Duration`、`Unique Time Played`以及`Video Segment`。

   1. 選取&#x200B;**[!UICONTROL 確認]**&#x200B;以儲存變更。

   1. 在&#x200B;**[!UICONTROL 結構]**&#x200B;區域中，啟用選項&#x200B;**[!UICONTROL 顯示欄位顯示名稱]**，然後選取`List Of Media Collection Downloaded Content Events`欄位。

   1. 選取&#x200B;**[!UICONTROL 管理相關欄位]**，然後依照下列方式更新結構描述：

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details`欄位中，隱藏下列報告欄位： `Ad Completed`、`Ad Started`和`Ad Time Played`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details`欄位中，隱藏下列報告欄位： `Ad Break ID`

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details`欄位中，隱藏下列報告欄位： `Chapter Completed`、`Chapter ID`、`Chapter Started`和`Chapter Time Played`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details`欄位中，隱藏`List Of States`欄位。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End`和`Media Collection Details` > `List Of States Start`欄位中，隱藏下列報告欄位： `Player State Count`、`Player State Set`和`Player State Time`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details`欄位中，隱藏下列報告欄位： `Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Events`、`Buffer Impacted Streams`、`Drops Before Starts`、`Dropped Frame Impacted Streams`、`Error Impacted Streams`、`Errors`、`External Error IDs`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Events`、`Stalling Impacted Streams`、`Total Buffer Duration`以及`Total Stalling Duration`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details`欄位中，隱藏下列報告欄位： `10% Progress Marker`、`25% Progress Marker`、`50% Progress Marker`、`75% Progress Marker`、`95% Progress Marker`、`Ad Count`、`Average Minute Audience`、`Chapter Count`、`Content Completes`、`Content Starts`、`Content Time Spent`、`Estimated Streams`、`Federated Data`、`Media Downloaded Flag`、`Media Segment Views`、`Media Session ID`、`Media Session Server Timeout`、`Media Starts`、`Media Time Spent`、`Pause Events`、`Pause Impacted Streams`、`Pccr`、`Pev3`、`Total Pause Duration`、`Unique Time Played`和`Video Segment`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details`欄位中，隱藏`Media Session ID`欄位。

   1. 選取&#x200B;**[!UICONTROL 確認]**&#x200B;以儲存變更。

   1. 在&#x200B;**[!UICONTROL 結構]**&#x200B;區域中，選取`Media Reporting Details`欄位，然後選取&#x200B;**[!UICONTROL 管理相關欄位]**。

   1. 啟用選項&#x200B;**[!UICONTROL 顯示欄位]**&#x200B;的顯示名稱，然後更新結構描述，如下所示：

      * 在`Media Reporting Details`欄位中，隱藏下列欄位： `Error Details`、`List Of States End`、`List of States Start`和`Media Session ID`。

   1. 選取&#x200B;**[!UICONTROL 確認]** > **[!UICONTROL 儲存]**&#x200B;以儲存變更。

   +++

1. （選用）您可以將自訂中繼資料新增到結構描述。 這可讓您針對特定需求或內容包含其他使用者定義的中繼資料。 如需使用Media Edge API自訂中繼資料的詳細資訊，請參閱[自訂中繼資料支援](custom-metadata.md)。

   +++ 展開以檢視將自訂中繼資料新增至結構描述的指示。

   1. 選取&#x200B;**[!UICONTROL 帳戶資訊]** > **[!UICONTROL 指派的組織]** > [!UICONTROL _&#x200B;**組織名稱**&#x200B;_] > **[!UICONTROL 租使用者]**，以找出組織的租使用者名稱稱。

      透過此路徑接收自訂欄位。 （例如，租使用者名稱稱： _dcbl → myCustomField路徑： _dcbl.myCustomField。）

   1. 新增自訂欄位群組至您定義的媒體結構描述。

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. 將您想要追蹤的任何自訂欄位新增至欄位群組。

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [使用產生的路徑](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties)作為要求承載中的自訂欄位。

      ![add-custom-metadata](assets/custom-fields-path.png)

   +++

## 在 Adobe Experience Platform 中建立資料集

1. 在Adobe Experience Platform中，依照[資料集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hant#create)中的說明開始建立資料集。

   為資料集選取結構描述時，請選擇您先前建立的結構描述。

## 在Adobe Experience Platform中設定資料串流

1. 如[設定資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hant)中所述，建立新的資料流。

   建立資料串流時，請進行下列選擇：

   * 在&#x200B;**[!UICONTROL 事件結構描述]**&#x200B;欄位中，選取您在[中建立的結構描述。在Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform)中設定結構描述。

     >[!IMPORTANT]
     >
     >選取&#x200B;**[!UICONTROL 儲存]**；不要選取&#x200B;**[!UICONTROL 儲存並新增對應]**。 選取&#x200B;**[!UICONTROL 儲存並新增對應]**&#x200B;會造成時間戳記欄位的對應錯誤。

     ![建立資料流並選取結構描述](assets/datastream-create-schema.png)

   * 根據您的Adobe解決方案，將適當的服務新增至資料流。 如需新增服務的相關資訊，請參閱[設定資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details)中的「將服務新增至資料流」。

      * **[!UICONTROL Adobe Analytics]** （若使用Adobe Analytics）：如[建立報表套裝](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)中所述，定義報表套裝。

      * **[!UICONTROL Adobe Experience Platform]** （若使用Customer Journey Analytics、Adobe Journey Optimizer或Real-Time Customer Data Platform）

     ![新增Adobe Analytics服務](assets/datastream-add-service.png)

   * 展開&#x200B;**[!UICONTROL 進階選項]**，然後啟用&#x200B;**[!UICONTROL Media Analytics]**&#x200B;選項。

     ![Media Analytics選項](assets/datastream-media-check.png)

## 選擇您的實作方法

在準備好結構、資料集和資料流後，實作下列其中一個程式碼庫，以開始將串流媒體資料傳送到Edge Network。 每個頁面都涵蓋串流媒體特定的設定；每個事件和每個變數的程式碼都存在於[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)中。

**程式碼內**&#x200B;實作會直接在應用程式原始碼中寫入SDK呼叫。 **使用標籤**&#x200B;實作使用[Adobe Experience Platform標籤](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)，可讓您設定及部署追蹤規則，而不需修改應用程式程式碼。 選擇適合您的部署工作流程的方法。

| 程式碼基底 | 程式碼內 | 使用標籤 |
|---|---|---|
| Web | [Web SDK](web-sdk.md) | [Web SDK標籤延伸模組](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS （標籤）](ios-tags.md) |
| Android | [Android](android.md) | [Android （標籤）](android-tags.md) |
| Roku | [Roku Edge](roku.md) | — |
| API | [Media Edge API](media-edge-api.md) | — |

## 下一步

開始收集資料後，您可以設定報表：

* [設定Edge實作的報表](/help/reporting/setup/edge-reporting.md) (Customer Journey Analytics)
* [為僅限Analytics的實施設定報告](/help/reporting/setup/analytics-reporting.md) （如果您的資料流摘要Adobe Analytics）

>[!MORELIKETHIS]
>
>* [自訂中繼資料支援](custom-metadata.md)
>* [XDM報告結構描述](reporting-schema.md)
>* [事件總覽](/help/implementation/events/overview.md)
