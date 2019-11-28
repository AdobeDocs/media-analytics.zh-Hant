---
title: 在 Chromecast 上追蹤核心播放
description: 本主題說明如何在 Chromecast 上使用 Media SDK 實作核心追蹤。
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 上追蹤核心播放{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>本文件涵蓋 SDK 2.x 版中的追蹤。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)

1. **初始追蹤設定**

   識別使用者何時觸發播放的意圖 (使用者點擊「播放」及/或開啟自動播放) 並建立 `MediaObject` 例項。

   **`MediaObject`API 參考資料:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`常數:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`常數:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **附加視訊中繼資料**

   可選擇透過內容資料變數，將標準和/或自訂視訊中繼資料物件附加到視訊追蹤工作階段。

   * **標準視訊中繼資料**

      [在 Chromecast 上實作標準中繼資料](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >將標準視訊中繼資料物件附加到媒體物件為選用。

   * **自訂中繼資料**

      為自訂變數建立變數物件，並為此視訊填入資料。例如:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **追蹤開始播放的意圖**

   若要開始追蹤媒體工作階段，請呼叫 `media` 物件上的 [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart)。

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 會追蹤使用者的播放意圖，而非播放的開始。此 API 用來載入視訊資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >秒數值是您在步驟 2 建立的自訂視訊中繼資料物件名稱。若您未使用自訂視訊中繼資料，只要對 `trackSessionStart` 中的 `data` 引數傳送空白物件即可，如上方 iOS 範例中的備註行所示。

1. **追蹤實際的播放開始**

   識別來自視訊播放器的視訊播放開始 (在畫面上轉譯了視訊的第一個時間格) 事件，並呼叫 [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **追蹤播放完成**

   識別來自視訊播放器的視訊播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **追蹤工作階段結尾**

   識別來自視訊播放器的視訊播放卸載/關閉 (使用者關閉視訊和/或視訊完成及卸載) 事件，並呼叫 [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 會標記視訊追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。除了新視訊追蹤工作階段的 `trackSessionStart` 外，在 `trackSessionEnd` 之後會忽略任何其他 `track*` API 呼叫。

1. **追蹤所有可能的暫停情況**

   識別來自視訊播放器視訊暫停的事件，並呼叫 [trackPause](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause):

   ```
   ADBMobile.media.trackPause();
   ```

   **暫停情況**

   識別視訊播放器將暫停的任何案例，並確定正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原影片。

1. 識別來自播放器的視訊播放和/或來自暫停的視訊恢復事件，並呼叫 [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >這可能與在步驟 4 使用的事件來源相同。在視訊播放繼續時，使用後續的 `trackPause()` API 呼叫確保 `trackPlay()` API 呼叫成對。

* 追蹤案例: [沒有廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的 Chromecast SDK 包含範例播放器。

