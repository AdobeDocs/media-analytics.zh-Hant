---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 測試 1: 標準播放{#test-standard-playback}

此測試案例可驗證一般播放和順序。這是認證申請表的一部分。

**請在這裡下載認證申請表：==&gt;**[認證申請表單。](cert_req_form.docx)

媒體實作由下列類型的追蹤呼叫組成：
* 媒體和廣告開始呼叫會直接傳送至AppMeasurement(Adobe Analytics)伺服器。
* 媒體Analytics心率呼叫會在開始時間和每10秒(針對內容)傳送，或每秒(用於廣告)傳送至Media Analytics追蹤伺服器。

>[!NOTE]
>所有平台的媒體追蹤行為相同。

您必須依下列順序完成並記錄這些動作：

1. **載入頁面或應用程式**

   **追蹤伺服器** (適用於所有網站與應用程式):

   * **AppMeasurement(Adobe Analytics)-** Experience Cloud訪客ID服務需要RDC追蹤伺服器或解析為RDC追蹤伺服器的CNAME。The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(Heartbeats)-** 此伺服器一律具有格式」`[namespace].hb.omtrdc.net`，其中 `[namespace]` 指定您的公司名稱。此名稱由Adobe提供。
   您需要驗證所有追蹤呼叫通用的主要變數：

   **Adobe訪客ID(`mid`)：**`mid` 變數會用來擷取AMCV Cookie中設定的值。`mid` 此變數是網站和行動應用程式的主要識別值，也表示Experience Cloud訪客ID服務已正確設定。它會在AppMeasurement和Media Analytics呼叫中找到。

   * **Media Analytics Play呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics Start呼叫**

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

   * **心率開始呼叫**

      | 參數 | 值 (範例) |
      |---|---|
      | `s:event:type` | start |

   * **VA 開始呼叫**

      >[!NOTE]
      >
      >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. 這沒有關係。They may not appear until the VA Play Calls ( `s:event:type=play`).

      | 參數 | 值 (範例) |
      |---|---|
      | `pev2` | ms_s |


1. **啓動媒體播放器**

   當媒體播放器開始時，索引鍵呼叫會依下列順序傳送：

   1. 媒體分析開始
   1. 心率開始
   1. 心率分析開始
   上述前兩個呼叫包含其他中繼資料和變數。如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md)

1. **檢視廣告插播 (可以的話)**

   * **廣告開始**
   當媒體廣告開始時，會以下列順序傳送下列索引鍵呼叫：

   1. 媒體廣告分析開始
   1. 心率廣告開始
   1. 心率廣告分析開始
   前兩個呼叫包含其他中繼資料和變數。如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **廣告播放**

      在廣告播放期間，心率呼叫會每隔一秒傳送到心率伺服器一次。

   * **廣告完成**

      在媒體廣告上的100%點，會傳送心率完整呼叫。



1. **暫停廣告播放 30 秒 (可以的話)。**  **廣告暫停**

   在廣告暫停期間，心率呼叫會每隔一秒傳送到心率伺服器一次。

   >[!NOTE]
   >
   >暫停時播放磁頭值應維持不變。

1. **不間斷地播放主要內容媒體10分鐘。**  **內容播放**

   在主要內容播放期間，心率呼叫每10秒會傳送至Media Analytics伺服器。

   附註:

   * 每個播放呼叫的播放點位置應該要以 10 為單位遞增。
   * `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

      如需呼叫參數和中繼資料，請參閱 [測試呼叫詳細資訊。](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **在播放期間暫停至少 30 秒。** 暫停媒體播放器時，暫停事件呼叫每10秒會傳送一次。暫停結束後，播放事件應該會繼續。

1. **尋找/拖曳媒體。** 在拖曳媒體播放磁頭時，不會傳送特殊追蹤呼叫，但是當拖曳播放磁頭值後，媒體播放繼續，應該反映主要內容內的新位置。

1. **重播媒體(僅限VOD)。** 當媒體重新播放時，應該傳送一組新的媒體開始呼叫，如同新媒體檢視一樣。

1. **在播放清單中檢視下一個媒體。** 在播放清單中的下一媒體媒體開始時，應該傳送新的媒體開始呼叫集。

1. **切換媒體或串流。**&#x200B;切換即時資料流時，不應傳送第一個資料流的心率完成呼叫。媒體開始呼叫和媒體play呼叫應以新顯示和串流名稱開始，並具有新顯示的正確播放磁頭和持續時間值。

