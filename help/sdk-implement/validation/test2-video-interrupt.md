---
seo-title: 測試視訊中斷
title: 測試視訊中斷
uuid: eeccd534-63fd-4dd3-b096-0431bc9 a11 ff
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 測試 2: 視訊中斷{#test-video-interruption}

本測試案例是憑證申請表單的必要內容，可用來驗證行動裝置中斷行為。

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

您必須依照以下順序完成這些工作並加以錄製:

1. **啟動視訊播放器**

   當視訊播放器開始時，以下呼叫的傳送順序如下:

   1. 媒體分析開始
   1. 心率開始
   1. 心率分析開始
   上述前兩個呼叫包含其他中繼資料和變數。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **播放主要內容視訊至少 5 分鐘並避免中斷**

   **內容播放**

   在正常主要內容播放期間，心率呼叫會每隔十秒傳送到心率伺服器一次。

   For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **將應用程式或瀏覽器移動到背景**

   從 VHL 1.6.6 版和更新版本開始，當應用程式在背景執行時，只應將 main:pause 呼叫傳送到心率伺服器。

1. **將應用程式或瀏覽器移動到背景**

   從背景返回時，應繼續播放內容。

1. **播放主要內容視訊至少 5 分鐘並避免中斷**

   For call parameters and metadata, see [Test Call Details.](/help/sdk-implement/validation/test-call-details.md)

1. **關閉視訊播放器**

   視訊播放器關閉後，不應觸發其他追蹤呼叫。

