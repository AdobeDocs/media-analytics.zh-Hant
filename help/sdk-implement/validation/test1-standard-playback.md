---
title: 測試1標準播放
description: 本主題說明在驗證中使用的標準播放測試。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 測試 1: 標準播放{#test-standard-playback}

此測試案例可驗證一般播放和順序。 這是您認證要求的必要元素。

## 認證申請表

**請從這裡下載認證申請表：==&gt;認**&#x200B;證 [申請表。](cert_req_form.docx)

## 認證測試1概觀

Media Analytics實作包含兩種類型的追蹤呼叫：
* 直接對您的Adobe Analytics(AppMeasurement)伺服器進行的呼叫——這些呼叫會發生在「媒體開始」和「廣告開始」事件上。
* 對媒體分析（心率）伺服器的呼叫——這些呼叫包括帶內和帶外呼叫：
   * 帶內- SDK會在內容播放期間以10秒間隔傳送計時播放呼叫或「ping」，並在廣告期間以1秒間隔傳送。
   * 帶外——這些呼叫可在任何時候發生，包括暫停、緩衝、錯誤、內容完成、廣告完成等。

>[!NOTE]
>媒體追蹤在所有平台上的運作都相同。

## 測試程式

完成並記錄下列動作（依順序）:

1. **載入頁面或應用程式**

   **追蹤伺服器** (適用於所有網站與應用程式):

   * **Adobe Analytics(AppMeasurement)伺服器** - Experience cloud訪客ID服務需要解析為RDC追蹤伺服器的RDC追蹤伺服器或CNAME。 The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **媒體分析(Heartbeats)伺服器** -此伺服器的格式一律為"`[namespace].hb.omtrdc.net`", `[namespace]` 指定您的公司名稱。 此名稱由Adobe提供。
   您必須驗證所有追蹤呼叫都通用的特定關鍵變數：

   **`mid`Adobe訪客ID(**):變 `mid` 數可用來擷取AMCV cookie中設定的值。 The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. 它可在Adobe Analytics(AppMeasurement)和Media Analytics（心率）呼叫中找到。

   * **Adobe Analytics Start呼叫**

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
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics開始呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >在「媒體分析開始」呼`s:event:type=start`叫中() `mid` 可能不存在值。 這沒有關係。直到「媒體分析播放」呼叫( `s:event:type=play`)才會顯示。

   * **媒體分析播放呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **啟動媒體播放器**

   當媒體播放器啟動時，Media SDK會依下列順序將金鑰呼叫傳送至兩部伺服器：

   1. Adobe Analytics伺服器——開始呼叫
   1. Media Analytics伺服器——開始呼叫
   1. Media Analytics伺服器- 「已要求Adobe Analytics開始呼叫」
   上述前兩個呼叫包含其他中繼資料和變數。 如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上述第三個呼叫會告訴Media Analytics伺服器，Media SDK要求將Adobe Analytics開始呼叫(`pev2=ms_s`)傳送至Adobe Analytics伺服器。

1. **檢視廣告插播 (可以的話)**

   * **廣告開始**
   當廣告開始時，會依下列順序傳送下列關鍵呼叫：

   1. Adobe Analytics伺服器——廣告開始呼叫
   1. Media Analytics伺服器——廣告開始呼叫
   1. Media Analytics伺服器- 「已要求Adobe Analytics廣告開始呼叫」
   前兩個呼叫包含其他中繼資料和變數。 如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   第三個呼叫會告訴Media Analytics伺服器，Media SDK要求將Adobe Analytics廣告開始呼叫(`pev2=msa_s`)傳送至Adobe Analytics伺服器。

   * **廣告播放**

      在廣告播放期間，Media Analytics SDK會每秒傳送「ad」類型的播放事件至Media Analytics伺服器。

   * **廣告完成**

      在廣告的100%點，應傳送媒體分析完整呼叫。



1. **暫停廣告播放 30 秒 (可以的話)。**  **廣告暫停**

   在「廣告暫停」期間，媒體分析心率或「ping」呼叫會由SDK每秒傳送至媒體分析伺服器。

   >[!NOTE]
   >
   >暫停期間，播放頭值應維持不變。

   如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **播放主要內容10分鐘不中斷。**  **內容播放**

   在主要內容播放期間，Media SDK會每10秒傳送心率（播放呼叫）至Media Analytics伺服器。

   附註:

   * 每次播放呼叫時，播放頭位置應增加10。
   * `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

      如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **在播放期間暫停至少 30 秒。** 在暫停媒體播放器時，SDK會每10秒傳送一次暫停事件呼叫至媒體分析伺服器。 暫停結束後，視訊將繼續播放。

   如需呼叫參數和中繼資料，請參閱「測 [試呼叫詳細資訊」。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **尋找／拖曳媒體。** 在拖曳媒體播放頭時，不會傳送任何特殊追蹤呼叫，但是，當媒體播放在拖曳後繼續時，播放頭值應反映主內容中的新位置。

1. **重播媒體（僅限VOD）。** 當重播媒體時，應傳送新的媒體開始呼叫集（如同新開始）。

1. **在播放清單中檢視下一個媒體。** 在播放清單中下一個媒體的「媒體開始」上，應傳送新的「媒體開始」呼叫集。

1. **切換媒體或串流。** 切換即時串流時，不應傳送媒體分析對第一個串流的完整呼叫。 「媒體開始」呼叫和「播放」呼叫應以新節目和串流名稱開頭，並使用新節目的正確播放磁頭和持續時間值。

