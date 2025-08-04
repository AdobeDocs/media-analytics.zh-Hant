---
title: 將Analytics來源聯結器實施移轉至更新的XDM串流媒體欄位
description: 瞭解如何將Analytics來源聯結器實作移轉至更新的XDM串流媒體欄位
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# 將Analytics來源聯結器實施更新至串流媒體的新的XDM欄位

>[!NOTE]
>
>此資訊適用於使用[Analytics來源聯結器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/adobe-applications/analytics)將串流媒體資料從Adobe Analytics帶入Adobe Experience Platform，以搭配Customer Journey Analytics報表或任何其他Platform服務的組織。
>
>這些變更不會影響Adobe Analytics作為獨立應用程式的效能，包括資料收集、處理和報告。 資料摘要和處理規則等工具不受影響，因此不需要更新Analytics實施。

適用於串流媒體服務的新Adobe Data Collection （Analytics來源聯結器）實作現在可以從一組XDM欄位遷移至另一組。

## 新XDM欄位路徑

在此移轉過程中，`mediaReporting` XDM欄位路徑已新增到Adobe資料收集（Analytics來源聯結器）流程中使用的XDM結構描述。 任何現有和新產生的Adobe資料收集結構描述將自動包含此新欄位。

## 取代舊的XDM欄位路徑

從Adobe Analytics將串流媒體資料傳輸到Adobe Experience Platform的所有Adobe資料收集（Analytics來源聯結器）流程目前都在新的`mediaReporting` XDM欄位路徑和舊的`media.mediaTimed` XDM欄位路徑上傳送資料。 這兩個欄位路徑都將在三個月後可用，直到2025年10月底。 10月後，`media.mediaTimed`欄位將完全棄用，10月後擷取的資料將僅包含`mediaReporting`。 棄用後，`media.mediaTimed`欄位將不再顯示在Adobe Experience Platform結構描述UI中，並且這些欄位上的資料擷取將停止。 因此，這些欄位將無法再用於任何Adobe Experience Platform服務。

在此日期之前擷取的資料將仍可用於報告。

## 與新XDM欄位路徑的其他差異

隨著適用於串流媒體的Adobe來源聯結器新實施，來自Adobe Analytics的持續呼叫現在會擷取到Adobe Experience Platform。

之前，這些呼叫不會反映在Customer Journey Analytics等平台應用程式中。 因此，您的組織可能會在報表中觀察到以下差異：

* **準確的工作階段計數**：在某些情況下，這可能表示工作階段計數減少，因為即使沒有直接的媒體互動，保持連線呼叫有助於維持作用中的使用者工作階段。 這些保持連線呼叫會在最後一個事件後的20分鐘內（根據媒體播放）產生，目的是保持造訪開啟。 若要確保Customer Journey Analytics中的最佳工作階段追蹤，建議在資料檢視中將造訪到期時間設定為30分鐘。

* **事件數增加**：因為保持連線呼叫現在計入Customer Journey Analytics事件量度中。 如果您想要從報表中排除保持連線呼叫，您可以建立篩選器，以排除事件型別為`media.keepalive`的事件。

此變更可確保Analytics與CJA報告之間更緊密地保持一致。

## 移轉現有的設定

為確保順利轉換，所有客戶必須在2025年10月底之前將現有設定從`media.mediaTimed`欄位移轉至`mediaReporting`欄位。 受影響的區域為依賴`media.mediaTimed`使用方式的區域，應依照下列各節所述進行移轉。

### Customer Journey Analytics**

CJA報表的移轉方式有兩種：

>[!NOTE]
>
>選擇下列選項之一後，您必須手動將Customer Journey Analytics報表中使用的每個`media.mediaTimed`欄位取代為對應衍生欄位或報表XDM欄位路徑。

* **若要保留歷史資料**： Adobe團隊已開發預先定義的Customer Journey Analytics範本，其中匯入一組衍生欄位，將舊版和新XDM欄位合併為單一欄位。 您可以根據Customer Journey Analytics連線要求，啟用此範本。 請聯絡Adobe支援團隊，協助您啟用新欄位。 這些衍生欄位不會計入貴組織的衍生欄位限制。

  若要檢視對應清單，請參閱[Adobe Experience Platform與Customer Journey Analytics的Media Analytics引數對應](/help/use-cases/xdm-updates/parameters-mapping.md)。

* **如果不需要歷史資料**：在報告時使用報告XDM欄位路徑就足夠了。 如需詳細資訊，請參閱[移轉Customer Journey Analytics以使用新的串流媒體欄位](/help/use-cases/xdm-updates/migrate-cja-setup.md)。

### Real-Time CDP

所有對象和設定檔都必須以`mediaReporting`為基礎。 如需詳細資訊，請參閱[將設定檔移轉至新的串流媒體欄位](/help/use-cases/xdm-updates/migrate-profiles.md)。

### 資料串流和資料收集

動態設定和資料對應必須使用`mediaReporting`。 如需詳細資訊，請參閱[將自訂欄位的資料準備移轉至新的串流媒體欄位](/help/use-cases/xdm-updates/migrate-dataprep.md)。

### 必須移轉的其他服務

* Adobe Journey Optimizer：行銷活動和歷程設定需要整合`mediaReporting`。

* 事件轉送：設定中只應包含`mediaReporting`欄位。

* 查詢服務：查詢必須參考`mediaReporting`欄位。

* 標籤設定：任何標籤設定都應參考`mediaReporting`欄位。

* 連線和目的地：匯入和匯出資料流程應圍繞`mediaReporting`欄位來建構。

請注意，依賴`media.mediaTimed`欄位的任何其他流程都會受到影響，並需要邏輯更新。

## 後續步驟與支援

所有使用適用於串流媒體的Adobe Data Collection的客戶都必須在指定的轉換期間內完成移轉。

如有任何問題或需要支援，請隨時聯絡Adobe支援團隊。

