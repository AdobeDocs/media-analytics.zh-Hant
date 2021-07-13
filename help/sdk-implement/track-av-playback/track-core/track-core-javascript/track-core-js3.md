---
title: 了解如何使用JavaScript 3.x版追蹤核心播放
description: 了解如何使用JavaScript 3.x應用程式，在瀏覽器中使用Media SDK實作核心追蹤。
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 95%

---

# 使用 JavaScript 3.x 追蹤核心播放{#track-core-playback-on-javascript}

>[!IMPORTANT]
>本文件涵蓋 SDK 3.x 版中的追蹤。若您正在實作任何舊版的 SDK，您可以在此處下載開發人員指南：[下載 SDK](/help/sdk-implement/download-sdks.md)。

1. **初始追蹤設定**

   識別使用者何時觸發播放的意圖 (使用者點擊「播放」及/或開啟自動播放) 並建立 `MediaObject` 例項。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 變數名稱 | 類型 | 說明 |
   | --- | --- | --- |
   | `name` | 字串 | 表示媒體名稱的非空白字串。 |
   | `id` | 字串 | 表示唯一媒體識別碼的非空白字串。 |
   | `length` | 數字 | 表示媒體秒數長度的正數。如果長度未知，請使用 0。 |
   | `streamType` | 字串 |  |
   | `mediaType` |  | 媒體類型 (音訊或視訊)。 |

   **`StreamType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `VOD` | 隨選視訊的資料流類型。 |
   | `AOD` | 隨選音訊的資料流類型。 |

   **`MediaType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `Audio` | 音效資料流的媒體類型。 |
   | `Video` | 視訊資料流的媒體類型。 |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **附加中繼資料**

   可選擇透過內容資料變數，將標準和/或自訂中繼資料附加到追蹤工作階段。

   * **標準中繼資料**

      >[!NOTE]
      >
      >附加標準中繼資料為選用。

      * 媒體中繼資料索引鍵 API 參考 - [標準中繼資料索引鍵 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         請在此處參閱完整的可用中繼資料組: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)
   * **自訂中繼資料**

      為自訂變數建立變數物件，並為此媒體填入資料。例如：

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **追蹤開始播放的意圖**

   若要開始追蹤媒體工作階段，請呼叫媒體心率例項上的 `trackSessionStart`:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 會追蹤使用者的播放意圖，而非播放的開始。此 API 用來載入資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >如果您未使用 contextData，只要為 `trackSessionStart` 中的 `data` 引數傳送空白物件即可。

1. **追蹤實際的播放開始**

   識別來自媒體播放器的播放開始 (在畫面上轉譯了媒體的第一個時間格) 事件，並呼叫 `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **追蹤播放完成**

   識別來自媒體播放器的播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **追蹤工作階段結尾**

   識別來自媒體播放器的播放卸載/關閉 (使用者關閉媒體和/或媒體完成及卸載) 事件，並呼叫 `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 會標記追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。在 `trackSessionEnd` 之後會忽略任何其他 `track*` API 呼叫 (除了新追蹤工作階段的 `trackSessionStart`)。

1. **追蹤所有可能的暫停情況**

   識別來自媒體播放器暫停的事件，並呼叫 `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **暫停情況**

   識別媒體播放器將暫停的任何案例，並確定正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原媒體。

1. 識別來自播放器的播放和/或來自暫停的恢復事件，並呼叫 `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >這可能與在步驟 4 使用的事件來源相同。確保播放恢復時，每個 `trackPause()` API 呼叫都與下列 `trackPlay()` API 呼叫成對。

* 追蹤案例：[沒有廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的含 JavaScript SDK 範例播放器。
