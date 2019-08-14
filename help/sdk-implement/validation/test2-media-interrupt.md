---
seo-title: 測試媒體中斷
title: 測試媒體中斷
uuid: eeccd534-63fd-4dd3-b096-0431bc9 a11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test2：媒體中斷{#test-media-interruption}

本測試案例是憑證申請表單的必要內容，可用來驗證行動裝置中斷行為。

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

您必須依照以下順序完成這些工作並加以錄製:

1. **啓動媒體播放器**

   當媒體播放器開始時，會以下列順序傳送下列呼叫：

   1. 媒體分析開始
   1. 心率開始
   1. 心率分析開始
   上述前兩個呼叫包含其他中繼資料和變數。如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md)

1. **播放主要內容媒體至少分鐘不間斷**

   **內容播放**

   在正常主要內容播放期間，心率呼叫會每隔十秒傳送到心率伺服器一次。

   如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **將應用程式或瀏覽器移動到背景**

   從 VHL 1.6.6 版和更新版本開始，當應用程式在背景執行時，只應將 main:pause 呼叫傳送到心率伺服器。

1. **將應用程式或瀏覽器移動到背景**

   從背景返回時，應繼續播放內容。

1. **播放主要內容媒體至少分鐘不間斷**

   如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md)

1. **關閉媒體播放器**

   在媒體播放器關閉後，不應引發其他追蹤呼叫。

