---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# 測試 1: 標準播放{#test-standard-playback}

此測試案例可驗證一般播放和順序。這是認證要求的必要元素。

## 認證申請表單

**請在這裡下載認證申請表：==&gt;**[認證申請表單。](cert_req_form.docx)

## Certification Test概觀

媒體分析實施包括兩種追蹤呼叫類型：
* 直接至您的Adobe Analytics(AppMeasurement)伺服器呼叫-這些呼叫會發生在「媒體開始」和「廣告開始」事件上。
* 對Media Analytics(活動訊號)伺服器的呼叫-包括節區內和帶外呼叫：
   * 節區- SDK會在內容播放期間以10秒間隔傳送計時播放呼叫或「縮圖」，並在廣告期間每隔秒傳送一次。
   * 帶外-這些呼叫可隨時發生，並包含暫停、緩衝、錯誤、內容完成、廣告完成等。

>[!NOTE]
>所有平台的媒體追蹤行為相同。

## 測試程序

完成並記錄下列動作(依序)：

1. **載入頁面或應用程式**

   **追蹤伺服器** (適用於所有網站與應用程式):

   * **Adobe Analytics(AppMeasurement)伺服器-** Experience Cloud訪客ID服務需要RDC追蹤伺服器或解析為RDC追蹤伺服器的CNAME。The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(Heartbeats)伺服器-** 此伺服器一律具有格式」`[namespace].hb.omtrdc.net`，其中 `[namespace]` 指定您的公司名稱。此名稱由Adobe提供。
   您需要驗證所有追蹤呼叫通用的主要變數：

   **Adobe訪客ID(`mid`)：**`mid` 變數會用來擷取AMCV Cookie中設定的值。`mid` 此變數是網站和行動應用程式的主要識別值，也表示Experience Cloud訪客ID服務已正確設定。這會在Adobe Analytics(AppMeasurement)和Media Analytics(活動訊號)呼叫中找到。

   * **Adobe Analytics開始呼叫**

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

   * **媒體分析開始呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >在Media Analytics Start呼叫(`s:event:type=start`) `mid` 中，值可能不存在。這沒有關係。在Media Analytics Play呼叫( `s:event:type=play`)之前，它們才會出現。

   * **Media Analytics Play呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **啓動媒體播放器**

   當媒體播放器開始時，Media SDK會依照下列順序傳送對這兩部伺服器的索引鍵呼叫：

   1. Adobe Analytics伺服器-開始呼叫
   1. 媒體分析伺服器-開始呼叫
   1. 媒體分析伺服器-「Adobe Analytics開始呼叫」已要求
   上述前兩個呼叫包含其他中繼資料和變數。如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   以上第三個呼叫告訴Media Analytics伺服器，Media SDK要求將Adobe Analytics Start(`pev2=ms_s`)呼叫傳送至Adobe Analytics伺服器。

1. **檢視廣告插播 (可以的話)**

   * **廣告開始**
   當廣告開始時，會以下列順序傳送下列索引鍵呼叫：

   1. Adobe Analytics伺服器-廣告開始呼叫
   1. 媒體分析伺服器-廣告開始呼叫
   1. 媒體分析伺服器-「已請求Adobe Analytics Ad Start呼叫」
   前兩個呼叫包含其他中繼資料和變數。如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   第三個呼叫告訴Media Analytics伺服器，Media SDK要求Adobe Analytics廣告開始呼叫(`pev2=msa_s`)傳送至Adobe Analytics伺服器。

   * **廣告播放**

      在廣告播放期間，Media Analytics SDK會每秒傳送「廣告」類型的「廣告」類型至Media Analytics伺服器。

   * **廣告完成**

      在廣告的100%點，應傳送媒體Analytics完整呼叫。



1. **暫停廣告播放 30 秒 (可以的話)。**  **廣告暫停**

   在「廣告暫停」期間，SDK會每秒傳送Media Analytics心率或「ping」呼叫至Media Analytics伺服器。

   >[!NOTE]
   >
   >暫停時播放磁頭值應維持不變。

   如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **不間斷地播放主要內容10分鐘。**  **內容播放**

   在主要內容播放期間，Media SDK每10秒會傳送心率(play呼叫)至Media Analytics伺服器。

   附註:

   * 播放磁頭位置在每次播放呼叫時應增加10。
   * `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

      如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **在播放期間暫停至少 30 秒。** 暫停媒體播放器時，每10秒SDK將會傳送暫停事件呼叫給Media Analytics伺服器。暫停結束後，視訊將繼續播放。

   如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **尋找/拖曳媒體。** 在拖曳媒體播放磁頭時，不會傳送特殊追蹤呼叫，但是當媒體播放在拖曳後繼續時，播放磁頭值應該反映主要內容內的新位置。

1. **重播媒體(僅限VOD)。** 當媒體重新播放時，應該傳送新的「媒體開始」呼叫(如同新的開始)。

1. **在播放清單中檢視下一個媒體。** 在播放清單中的下一媒體媒體開始時，應該傳送新的媒體開始呼叫集。

1. **切換媒體或串流。** 切換即時串流時，不應傳送第一個串流的Media Analytics完整呼叫。「媒體開始」呼叫和「播放」呼叫應以新顯示和串流名稱開始，並具有新顯示的正確播放磁頭和持續時間值。

