---
title: 測試 1 標準播放
description: 了解驗證作業使用的標準播放測試。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '838'
ht-degree: 100%

---

# 測試 1：標準播放{#test-standard-playback}

本測試案例可用來驗證一般播放和序列是否正常。

Media Analytics 實作包含兩種類型的追蹤呼叫：
* 直接對 Adobe Analytics (AppMeasurement) 伺服器進行的呼叫 - 這些呼叫會在「媒體開始」和「廣告開始」事件中發生。
* 對 Media Analytics (心率) 伺服器進行呼叫 - 這些包含頻內和頻外呼叫。
   * 頻內 - SDK 會在內容播放期間以 10 秒的間隔並在廣告期間以 1 秒的間隔傳送播放時間呼叫或「Ping」。
   * 頻外 - 這些呼叫會在任何時間點發生，且會包含暫停、緩衝處理、錯誤、內容完成和廣告完成等。

>[!NOTE]
>媒體追蹤的行為在所有平台上都一樣。

## 測試程序

完成並記錄下列動作 (依序)：

1. **載入頁面或應用程式**

   **追蹤伺服器** (適用於所有網站與應用程式)：

   * **Adobe Analytics (AppMeasurement) 伺服器 -** Experience Cloud 訪客 ID 服務須有 RDC 追蹤伺服器，或是解析為 RDC 追蹤伺服器的 CNAME。Adobe Analytics 追蹤伺服器的結尾應該是「`.sc.omtrdc.net`」或應該是 CNAME。

   * **Media Analytics (心率) 伺服器 -** 這部伺服器的格式一律為「`[namespace].hb.omtrdc.net`」，其中 `[namespace]` 會指定您的公司名稱。此名稱由 Adobe 提供。

   您需要驗證所有追蹤呼叫的某些重要通用變數：

   **Adobe 訪客 ID (`mid`)：** `mid` 變數可以用來擷取 AMCV Cookie 中設定的值。`mid` 變數是網站與行動應用程式的主要識別值，也代表 Experience Cloud 訪客 ID 服務設定正確。您可以在 Adobe Analytics (AppMeasurement) 與 Media Analytics (心率) 呼叫中找到它。

   * **Adobe Analytics 開始呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **網站頁面呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **生命週期呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `pev2` | ADBINTERNAL：Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics 開始呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >`mid` 值不一定會存在 Media Analytics 開始呼叫 (`s:event:type=start`) 中。這沒有關係。在 Media Analytics 播放呼叫 (`s:event:type=play`) 之前，它們不一定會出現。

   * **Media Analytics 播放呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **啟動媒體播放器**

   當媒體播放器啟動時，Media SDK 會依照下列順序將重要的呼叫傳送給兩個伺服器：

   1. Adobe Analytics 伺服器 - 開始呼叫
   1. Media Analytics 伺服器 - 開始呼叫
   1. Media Analytics 伺服器 -「已要求 Adobe Analytics 開始呼叫」

   以上前兩個呼叫含有額外的中繼資料和變數。如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#start-the-media-player)。

   以上第三個呼叫會通知 Media Analytics 伺服器，Media SDK 已要求將 Adobe Analytics 開始呼叫 (`pev2=ms_s`) 傳送到 Adobe Analytics 伺服器。

1. **檢視廣告插播 (可以的話)**

   * **廣告開始**

   當廣告開始時，重要呼叫的傳送順序如下：

   1. Adobe Analytics 伺服器 - 廣告開始呼叫
   1. Media Analytics 伺服器 - 廣告開始呼叫
   1. Media Analytics 伺服器 -「已要求 Adobe Analytics 廣告開始呼叫」

   前兩個呼叫含有額外的中繼資料和變數。如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#view-ad-playback)。

   第三個呼叫會通知 Media Analytics 伺服器，Media SDK 已要求將 Adobe Analytics 廣告開始呼叫 (`pev2=msa_s`) 傳送到 Adobe Analytics 伺服器。

   * **廣告播放**

      在廣告播放期間，Media Analytics SDK 每秒都會將「廣告」類型的的播放事件傳送到 Media Analytics 伺服器。

   * **廣告完成**

      在廣告的 100% 點上，應傳送 Media Analytics 完成呼叫。



1. **暫停廣告播放 30 秒 (可以的話)。**  **廣告暫停**

   在廣告暫停期間，SDK 會每秒將 Media Analytics 心率或「Ping」呼叫傳送到 Media Analytics 伺服器。

   >[!NOTE]
   >
   >播放點值在暫停期間應保持不變。

   如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)。

1. **播放主要內容 10 秒鐘並避免中斷。**  **內容播放**

   在主要內容播放期間，Media SDK 會每隔 10 秒將心率 (播放呼叫) 傳送到 Media Analytics 伺服器。

   附註：

   * 每個「播放」呼叫的播放點位置應該要以 10 為單位遞增。
   * `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

      如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#play-main-content)。

1. **在播放期間暫停至少 30 秒。** 暫停媒體播放器時，SDK 會每隔 10 秒將暫停事件呼叫傳送到 Media Analytics 伺服器。暫停結束後，視訊將繼續播放。

   如需呼叫參數與中繼資料的相關資訊，請參閱[測試呼叫詳細資料](/help/legacy/validation/test-call-details.md#pause-main-content)。

1. **尋找/拖曳媒體。**&#x200B;拖曳媒體播放點時，不會傳送任何特殊的追蹤呼叫，不過當拖曳結束後繼續播放媒體時，播放點值應該要反映主要內容中的新位置。

1. **重播媒體 (僅限 VOD)。**&#x200B;重播媒體時，應傳送一組新的媒體開始呼叫 (就像重新開始一樣)。

1. **檢視播放清單中的下一個媒體。**&#x200B;開始播放播放清單中的下一個媒體時，應傳送一組新的媒體開始呼叫。

1. **切換媒體或資料流。**&#x200B;切換即時資料流時，不應傳送第一個資料流的 Media Analytics 心率完成呼叫。媒體開始呼叫和播放呼叫的開頭，應該要是新節目和資料流名稱，以及新節目的正確播放點和持續時間值。
