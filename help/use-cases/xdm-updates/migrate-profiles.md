---
title: 將設定檔移轉至新的串流媒體欄位
description: 瞭解如何將設定檔移轉至新的串流媒體欄位
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 0%

---

# 將設定檔移轉至新的串流媒體欄位

本檔案說明移轉設定檔篩選服務的程式，該服務是位於為Adobe Analytics啟用串流媒體資料的Adobe資料收集流程之上。 移轉會將設定檔篩選服務從使用名為「媒體」的Adobe串流媒體服務資料型別轉換為使用名為「[媒體報表詳細資料](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)」的新對應資料型別。

## 移轉設定檔

若要將設定檔篩選從名為「媒體」的舊資料型別移轉到名為「[媒體報告詳細資料](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/media-reporting-details)」的新資料型別，您必須編輯現有的設定檔篩選規則：

1. 在Adobe Experience Platform中的&#x200B;[!UICONTROL **來源**]&#x200B;區段底下，前往&#x200B;[!UICONTROL **資料流**]&#x200B;標籤。

1. 找出負責透過Adobe Data Collection將串流媒體資料從Adobe Analytics匯入Adobe Experience Platform的資料流。

1. 選取&#x200B;[!UICONTROL **更新資料流**]，將包含已棄用欄位的每個自訂規則取代為新XDM物件中新的對應欄位，以修改設定檔篩選設定。

1. 找出包含已棄用「媒體」物件欄位的篩選器。

1. 從新的「媒體報告詳細資訊」物件新增欄位，以附加這些篩選器。

1. 在兩個欄位之間使用OR運運算元；

1. 驗證設定檔是否仍如預期般運作。

檢視[內容ID](/help/reporting/dimensions/content.md)引數和[串流媒體服務](/help/media-overview.md)下記錄的其餘串流媒體變數，以對應舊欄位和新欄位。 舊欄位路徑可在「XDM欄位路徑」屬性下找到，而新欄位路徑可在「報告XDM欄位路徑」屬性下找到。

## 範例

為了更方便遵循移轉准則，請考慮以下包含單一設定檔篩選規則的資料流範例。 在此情況下，由於只有單一規則，因此您只需要套用移轉指引一次。

1. 在Adobe Experience Platform中的&#x200B;[!UICONTROL **來源**]&#x200B;區段底下，前往&#x200B;[!UICONTROL **資料流**]&#x200B;標籤。

1.找出負責透過Adobe Analytics將串流媒體資料從Adobe Analytics匯入Adobe Experience Platform的資料流。

1. 選取&#x200B;**[!UICONTROL 更新資料流]**&#x200B;以輸入編輯使用者介面，如下圖所示。

   ![AEP資料流設定檔](assets/aep-dataflow-profile.jpeg)

1. 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以移至[篩選]索引標籤。

   ![AEP資料流篩選器索引標籤](assets/aep-dataflow-filtering-profile.jpeg)

1. 在&#x200B;**[!UICONTROL 篩選]**&#x200B;索引標籤上，識別依賴`media.mediaTimed`欄位的篩選規則。

   ![AEP資料流篩選規則](assets/dataflow-filtering-rules-profile.jpeg)


   對於使用meda.mediaTimed物件的每個篩選器，在`mediaReporting`物件中，使用[串流媒體服務](/help/media-overview.md)下記錄的串流媒體變數找到其對應項，以對應舊欄位和新欄位。 舊欄位路徑可在「XDM欄位路徑」屬性下找到，而新欄位路徑可在「報告XDM欄位路徑」屬性下找到。 例如，對於[Media Starts](/help/reporting/metrics/media-starts.md)，`media.mediaTimed.impressions.value`的通訊者是`mediaReporting.sessionDetails.isViewed`。

   ![新舊的XDM欄位](assets/xdm-fields-new-and-old.jpeg)

1. 將相關的`mediaReporting`欄位拖曳至篩選規則，並在兩個規則之間使用OR運運算元。 使用新欄位時新增與現有規則相同的規則。

   ![新增篩選器規則](assets/add-filter-rules.jpeg)

1. 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以儲存變更。
