---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 測試 1: 標準播放{#test-standard-playback}

此測試案例可驗證一般播放和順序，並為認證申請表的一部分。Download the certification request form here: [Certification Request Form.](cert_req_form_nielsen.docx)

視訊實作由以下類型的追蹤呼叫所組成:
* 視訊和廣告開始呼叫會直接傳送到 AppMeasurement 伺服器。
* 媒體分析(MA)心率呼叫會每隔10秒傳送至Adobe VA追蹤伺服器。

>[!NOTE]
>視訊追蹤的行為在所有平台、桌上型電腦及行動裝置上都一樣。

您必須依照以下順序完成動作並加以錄製:

1. **載入頁面或應用程式**

   **追蹤伺服器** (適用於所有網站與應用程式):

   * **AppMeasurement (Adobe Analytics) -** Experience Cloud 訪客 ID 服務須有 RDC 追蹤伺服器，或是解析為 RDC 伺服器的 CNAME。The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **媒體分析(活動訊號)-** 此伺服器一律具有格式 `[namespace].hb.omtrdc.net`，由 `[namespace]` 您的登入公司定義，由Adobe提供。
   您需要在所有追蹤呼叫中驗證特定的關鍵、通用變數：

   **Adobe訪客ID(`mid`)：**`mid` 變數會用來擷取AMCV Cookie中設定的值。`mid` 此變數是網站和行動應用程式的主要識別值，也表示Experience Cloud訪客ID服務已正確設定。它會在AppMeasurement和Media Analytics(MA)呼叫中找到。

   * **心率播放呼叫**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. 這沒有關係。They may not appear until the VA Play Calls ( `s:event:type=play`).

      | 參數 | 值 (範例) |
      |---|---|
      | `pev2` | ms_s |


1. **啟動視訊播放器**

   當視訊播放器開始時，重要呼叫的傳送順序如下:

   1. 視訊分析開始
   1. 心率開始
   1. 心率分析開始
   上述前兩個呼叫包含其他中繼資料和變數。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **檢視廣告插播 (可以的話)**

   * **廣告開始**
   當視訊廣告開始時，重要呼叫的傳送順序如下:

   1. 視訊廣告分析開始
   1. 心率廣告開始
   1. 心率廣告分析開始
   前兩個呼叫包含其他中繼資料和變數。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **廣告播放**

      在廣告播放期間，心率呼叫會每隔一秒傳送到心率伺服器一次。

   * **廣告完成**

      心率完成呼叫會在視訊廣告到達 100% 的點時傳送。



1. **暫停廣告播放 30 秒 (可以的話)。**  **廣告暫停**

   在廣告暫停期間，心率呼叫會每隔一秒傳送到心率伺服器一次。

   >[!NOTE]
   >
   >暫停時播放磁頭值應維持不變。

1. **播放主要內容視訊 10 分鐘並避免中斷。** **內容播放 **

   在正常主要內容播放期間，心率呼叫會每隔十秒傳送到心率伺服器一次。

   附註:

   * 每個播放呼叫的播放點位置應該要以 10 為單位遞增。
   * `l:event:duration` 值代表上一個追蹤呼叫距離現在的毫秒數，應該要每個 10 秒鐘呼叫大致相同。

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **在播放期間暫停至少 30 秒。**&#x200B;暫停視訊播放器時，暫停事件呼叫會每隔 10 秒傳送一次。暫停結束後，播放事件應該會繼續。

1. **尋找/拖曳視訊。**&#x200B;拖曳視訊播放點時，不會傳送任何特殊的追蹤呼叫，不過當拖曳結束後繼續播放視訊時，播放點值應該要反應主要內容中的新位置。

1. **重播視訊 (僅限 VOD)。**&#x200B;重播視訊時，應傳送一組新的視訊開始呼叫，就像全新的視訊檢視一樣。

1. **檢視播放清單中的下一部視訊。**&#x200B;開始播放播放清單中的下一部視訊時，應傳送一組新的視訊開始呼叫。

1. **切換視訊或資料流。**&#x200B;切換即時資料流時，不應傳送第一個資料流的心率完成呼叫。視訊開始呼叫和視訊播放呼叫的開頭，應該要是新節目和資料流名稱，以及新節目的正確播放點和持續時間值。

