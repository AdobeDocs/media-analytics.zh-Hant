---
title: 了解如何使用JavaScript 2.x追蹤核心播放
description: 了解如何使用JavaScript 2.x應用程式，在瀏覽器中使用Media SDK實作核心追蹤。
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 94%

---

# 使用 JavaScript 2.x 追蹤核心播放{#track-core-playback-on-javascript}

下列指示提供在2.x SDK間實作的指引。

>[!IMPORTANT]
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)

1. **初始追蹤設定**

   識別使用者何時觸發播放的意圖 (使用者點擊「播放」及/或開啟自動播放) 並建立 `MediaObject` 例項。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 媒體名稱 | 是 |
   | `mediaid` | 媒體唯一識別碼 | 是 |
   | `length` | 媒體長度 | 是 |
   | `streamType` | 資料流類型 (請參閱下列 _StreamType 常數_) | 是 |
   | `mediaType` | 媒體類型 (請參閱下列 _MediaType 常數_) | 是 |

   **`StreamType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `VOD` | 隨選視訊的資料流類型。 |
   | `LIVE` | LIVE 內容的資料流類型。 |
   | `LINEAR` | LINEAR 內容的資料流類型。 |
   | `AOD` | 隨選音訊的資料流類型。 |
   | `AUDIOBOOK` | 有聲書的資料流類型. |
   | `PODCAST` | 播客的資料流類型. |

   **`MediaType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `Audio` | 音效資料流的媒體類型。 |
   | `Video` | 視訊資料流的媒體類型。 |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **附加中繼資料**

   可選擇透過內容資料變數，將標準和/或自訂中繼資料物件附加到追蹤工作階段。

   * **標準中繼資料**

      [在 JavaScript 上實作標準中繼資料](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >將標準中繼資料物件附加到媒體物件為選用。

      * 媒體中繼資料索引鍵 API 參考 - [標準中繼資料索引鍵 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         請在此處參閱完整的可用中繼資料組: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)
   * **自訂中繼資料**

      為自訂變數建立變數物件，並為此媒體填入資料。例如：

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **追蹤開始播放的意圖**

   若要開始追蹤媒體工作階段，請呼叫媒體心率例項上的 `trackSessionStart`:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >秒數值是您在步驟 2 建立的自訂媒體中繼資料物件名稱。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 會追蹤使用者的播放意圖，而非播放的開始。此 API 用來載入資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >若您未使用自訂中繼資料，只要對 `trackSessionStart` 中的 `data` 引數傳送空白物件即可，如上方 iOS 範例中的備註行所示。

1. **追蹤實際的播放開始**

   識別來自媒體播放器的播放開始 (在畫面上轉譯了媒體的第一個時間格) 事件，並呼叫 `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **追蹤播放完成**

   識別來自媒體播放器的播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **追蹤工作階段結尾**

   識別來自媒體播放器的播放卸載/關閉 (使用者關閉媒體和/或媒體完成及卸載) 事件，並呼叫 `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 會標記追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。在 `trackSessionEnd` 之後會忽略任何其他 `track*` API 呼叫 (除了新追蹤工作階段的 `trackSessionStart`)。

1. **追蹤所有可能的暫停情況**

   識別來自媒體播放器暫停的事件，並呼叫 `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **暫停情況**

   識別媒體播放器將暫停的任何案例，並確定正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原媒體。

1. 識別來自播放器的播放和/或來自暫停的恢復事件，並呼叫 `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >這可能與在步驟 4 使用的事件來源相同。確保播放恢復時，每個 `trackPause()` API 呼叫都與下列 `trackPlay()` API 呼叫成對。

* 追蹤案例：[沒有廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的含 JavaScript SDK 範例播放器。
