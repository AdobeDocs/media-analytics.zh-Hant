---
seo-title: 測試2媒體中斷
title: 測試2媒體中斷
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# 測試2:媒體中斷{#test-media-interruption}

此測試案例可驗證行動中斷行為。 這是您認證要求的必要元素。

## 認證申請表

**請從這裡下載認證申請表：==&gt;認**&#x200B;證 [申請表。](cert_req_form.docx)

## 測試程式

您必須依照以下順序完成這些工作並加以錄製:

1. **啟動媒體播放器**

   媒體播放器啟動時，會依下列順序傳送下列呼叫：

   1. Adobe Analytics(AppMeasurement)開始
   1. 媒體分析（心率）開始
   1. 請求Media Analytics（心率）Adobe Analytics start呼叫
   上述前兩個呼叫包含其他中繼資料和變數。 如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上述第三個呼叫會告訴Media Analytics伺服器，Media SDK要求將Adobe Analytics開始呼叫(`pev2=ms_s`)傳送至Adobe Analytics伺服器。

1. **播放主要內容至少5分鐘不中斷**

   **內容播放**

   在內容播放期間，Media SDK會每十秒傳送播放呼叫（心率）至Media Analytics伺服器。

   如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **將應用程式或瀏覽器移動到背景**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **將應用程式或瀏覽器帶回前景**

   從背景返回時，應繼續播放內容。

1. **播放主要內容媒體至少5分鐘不中斷**

   如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **關閉媒體播放器**

   媒體播放器關閉後，不應觸發其他追蹤呼叫。

