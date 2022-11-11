---
title: 測試2：媒體中斷
description: 了解用於驗證的媒體中斷測試。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 89%

---

# 測試 2：媒體中斷{#test-media-interruption}

本測試案例可用來驗證行動裝置中斷行為。

## 測試程序

您必須依照以下順序完成這些工作並加以錄製:

1. **啟動媒體播放器**

   當媒體播放器開始時，以下呼叫的傳送順序如下:

   1. Adobe Analytics (AppMeasurement) 開始
   1. Media Analytics (心率) 開始
   1. 已要求 Media Analytics (心率) Adobe Analytics 開始呼叫

   以上前兩個呼叫含有額外的中繼資料和變數。如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#start-the-media-player)。

   以上第三個呼叫會通知 Media Analytics 伺服器，Media SDK 已要求將 Adobe Analytics 開始呼叫 (`pev2=ms_s`) 傳送到 Adobe Analytics 伺服器。

1. **播放主要內容至少 5 分鐘並避免中斷**

   **內容播放**

   在內容播放期間，Media SDK 會每隔十秒將播放呼叫 (心率) 傳送到 Media Analytics 伺服器。

   如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#play-main-content)。

   另請參閱平台的 [追蹤廣告](/help/use-cases/track-ads/track-ads-overview.md) 這些廣告呼叫的其他資訊指示。

1. **將應用程式或瀏覽器移動到背景**

   從 VHL 1.6.6 版和更新版本開始，當應用程式在背景執行時，只應將 `main:pause` 呼叫傳送到 Media Analytics 伺服器。

1. **將應用程式或瀏覽器移回前景**

   從背景返回時，應繼續播放內容。

1. **播放主要內容媒體至少 5 分鐘並避免中斷**

   如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#play-main-content)。

1. **關閉媒體播放器**

   媒體播放器關閉後，不應觸發其他追蹤呼叫。
