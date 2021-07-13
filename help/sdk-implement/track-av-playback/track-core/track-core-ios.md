---
title: 了解如何在iOS上追蹤核心播放
description: 了解如何在iOS上使用Media SDK實作核心追蹤。
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 95%

---

# 在 iOS 上追蹤核心播放{#track-core-playback-on-ios}

>[!IMPORTANT]
>本文件涵蓋 SDK 2.x 版中的追蹤。若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)

1. **初始追蹤設定**

   識別使用者何時觸發播放的意圖 (使用者點擊「播放」及/或開啟自動播放) 並建立 `MediaObject` 例項。

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 變數名稱 | 說明 | 必填 |
   |---|---|---|
   | `name` | 視訊名稱 | 是 |
   | `mediaid` | 視訊唯一識別碼 | 是 |
   | `length` | 視訊長度 | 是 |
   | `streamType` | 資料流類型 (請參閱下列 _StreamType 常數_) | 是 |
   | `mediaType` | 媒體類型 (請參閱下列 _MediaType 常數_) | 是 |

   **`StreamType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | 隨選視訊的資料流類型 |
   | `ADBMediaHeartbeatStreamTypeLIVE` | 直播內容的資料流類型 |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | 線性播出內容的資料流類型 |
   | `ADBMediaHeartbeatStreamTypeAOD` | 隨選音效的資料流類型 |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | 有聲書的資料流類型 |
   | `ADBMediaHeartbeatStreamTypePODCAST` | 播客的資料流類型 |

   **`MediaType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `ADBMediaTypeAudio` | 音效資料流的媒體類型。 |
   | `ADBMediaTypeVideo` | 視訊資料流的媒體類型。 |

   建立 `MediaObject` 的一般格式:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **附加視訊中繼資料**

   可選擇透過內容資料變數，將標準和/或自訂視訊中繼資料物件附加到視訊追蹤工作階段。

   * **標準視訊中繼資料**

      * [在 iOS 上實作標準中繼資料](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **視訊中繼資料索引鍵**

         [iOS 中繼資料索引鍵](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * 請在這裡參閱完整的視訊中繼資料清單: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >將標準視訊中繼資料物件附加到媒體物件為選用。

   * **自訂中繼資料**

      為自訂變數建立變數物件，並為此視訊填入資料。例如:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **追蹤開始播放的意圖**

   若要開始追蹤媒體工作階段，請呼叫媒體心率例項上的 `trackSessionStart`。

   >[!TIP]
   >
   >秒數值是您在步驟 2 建立的自訂視訊中繼資料物件名稱。

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 會追蹤使用者的播放意圖，而非播放的開始。此 API 用來載入視訊資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >若您未使用自訂視訊中繼資料，只要對 `trackSessionStart` 中的 `data` 引數傳送空白物件即可，如上方 iOS 範例中的備註行所示。

1. **追蹤實際的播放開始**

   識別來自視訊播放器的視訊播放開始 (在畫面上轉譯了視訊的第一個時間格) 事件，並呼叫 `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **追蹤播放完成**

   識別來自視訊播放器的視訊播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **追蹤工作階段結尾**

   識別來自視訊播放器的視訊播放卸載/關閉 (使用者關閉視訊和/或視訊完成及卸載) 事件，並呼叫 `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 會標記視訊追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。除了新視訊追蹤工作階段的 `trackSessionStart` 外，在 `trackSessionEnd` 之後會忽略任何其他 `track*` API 呼叫。

1. **追蹤所有可能的暫停情況**

   識別來自視訊播放器視訊暫停的事件，並呼叫 `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **暫停情況**

   識別視訊播放器將暫停的任何案例，並確定正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原影片。

1. 識別來自播放器的視訊播放和/或來自暫停的視訊恢復事件，並呼叫 `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >這可能與在步驟 4 使用的事件來源相同。在視訊播放繼續時，使用後續的 `trackPause()` API 呼叫確保 `trackPlay()` API 呼叫成對。

如需有關追蹤核心播放的詳細資訊，請參閱下列內容:

* 追蹤案例：[沒有廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的 iOS SDK 包含範例播放器。
