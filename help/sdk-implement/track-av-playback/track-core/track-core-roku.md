---
seo-title: 在 Roku 上追蹤核心播放
title: 在 Roku 上追蹤核心播放
uuid: a8aa7b3c-2d39-44d-7ebc-b101 d130101 f
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# 在 Roku 上追蹤核心播放{#track-core-playback-on-roku}

>[!IMPORTANT]
>本文件涵蓋SDK2.x版追蹤。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](../../../sdk-implement/download-sdks.md)

1. **初始追蹤設定**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`參考：**

   | 變數名稱 | 說明 | 必要 |
   | --- | --- | :---: |
   | `name` | 視訊名稱 | 是 |
   | `mediaid` | 視訊唯一識別碼 | 是 |
   | `length` | 視訊長度 | 是 |
   | `streamType` | Stream type (see _StreamType constants_ below) | 是 |
   | `mediaType` | Media type (see _MediaType constants_ below) | 是 |

   **`StreamType`常數：**

   | 常數名稱 | 說明   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | 隨選視訊的資料流類型。 |
   | `MEDIA_STREAM_TYPE_LIVE` | LIVE 內容的資料流類型。 |
   | `MEDIA_STREAM_TYPE_LINEAR` | LINEAR 內容的資料流類型。 |
   | `MEDIA_STREAM_TYPE_AOD` | 隨選音效的資料流類型 |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | 有聲書的資料流類型 |
   | `MEDIA_STREAM_TYPE_PODCAST` | 播客的資料流類型 |

   **`MediaType`常數：**

   | 常數名稱 | 說明 |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | 音效資料流的媒體類型。 |
   | `MEDIA_STREAM_TYPE_VIDEO` | 視訊資料流的媒體類型。 |

   **使用VOD內容建立視訊的媒體資訊物件：**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   或 

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **使用AOD內容建立視訊的媒體資訊物件：**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   或 

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **附加中繼資料**

   (選擇性)透過上下文資料變數，將標準和/或自訂中繼資料物件附加至追蹤工作階段。

   * **標準中繼資料**

      [在 JavaScript 上實作標準中繼資料](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >將標準中繼資料物件附加至媒體物件是選擇性的。

      * 媒體中繼資料索引鍵 API 參考 - [標準中繼資料索引鍵 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
   * **自訂中繼資料**

      建立自訂變數的變數物件，並填入此媒體的資料。例如:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **追蹤開始播放的意圖**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >第二個值是您在步驟建立的自訂媒體中繼資料物件名稱。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 追蹤使用者的播放意圖，而不是播放的開始。此 API 用來載入資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **追蹤實際播放的開始**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **追蹤播放完成**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **追蹤作業結束**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. 如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  媒體播放追蹤方法以追蹤媒體負載並將目前的作業設定為作用中:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **附加視訊中繼資料**

   (選擇性)透過上下文資料變數，將標準和/或自訂視訊中繼資料物件附加至視訊追蹤工作階段。

   * **標準視訊中繼資料**

      [在 Roku 上實作標準中繼資料](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >將標準視訊中繼資料物件附加至媒體物件是選擇性的。

   * **自訂中繼資料**

      建立自訂變數的變數物件，並填入此視訊的資料。例如:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **追蹤開始播放的意圖**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >第二個值是您在步驟建立的自訂視訊中繼資料物件名稱。

   >[!IMPORTANT]
   >`trackSessionStart` 追蹤使用者的播放意圖，而不是播放的開始。此 API 用來載入視訊資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **追蹤實際播放的開始**

   識別來自視訊播放器的視訊播放開始 (在畫面上轉譯了視訊的第一個時間格) 事件，並呼叫 `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **追蹤播放完成**

   識別來自視訊播放器的視訊播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **追蹤作業結束**

   識別來自視訊播放器的視訊播放卸載/關閉 (使用者關閉視訊和/或視訊完成及卸載) 事件，並呼叫 `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` 標示視訊追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **追蹤所有可能的暫停案例**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **暫停藍本**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原影片。

1. 識別來自播放器的視訊播放和/或來自暫停的視訊恢復事件，並呼叫 `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >這可能與步驟中使用的事件來源相同。在視訊播放繼續時，使用後續的 `trackPause()` API 呼叫確保 `trackPlay()` API 呼叫成對。

* 追蹤案例: [沒有廣告的 VOD 播放](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的 Roku SDK 包含範例播放器。

