---
seo-title: 追蹤概述
title: 追蹤概述
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 追蹤概述{#tracking-overview}

>[!IMPORTANT]
>
>本檔案涵蓋SDK 2.x版的追蹤。 若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK.](/help/sdk-implement/download-sdks.md)

## 播放器事件

追蹤核心播放包含追蹤媒體載入、媒體開始、媒體暫停和媒體完成。雖然並非為強制性，但追蹤緩衝和搜尋也為可用於追蹤內容播放的核心元件。在您的媒體播放器 API 中，識別與 Media SDK 追蹤呼叫對應的播放器事件，並編寫事件處理程式的程式碼，以呼叫追蹤 API 及填入必要和選用的變數。

### 媒體載入時

* 建立媒體物件
* 填入中繼資料
* 電 `trackSessionStart`話；例如： `trackSessionStart(mediaObject, contextData)`

### 媒體開始時

* 呼叫 `trackPlay`

### 暫停/繼續時

* 呼叫 `trackPause`
* Call `trackPlay`   _when playback resumes_

### 媒體完成時

* 呼叫 `trackComplete`

### 媒體中止時

* 呼叫 `trackSessionEnd`

### 拖曳開始時

* 呼叫 `trackEvent(SeekStart)`

### 拖曳結束時

* 呼叫 `trackEvent(SeekComplete)`

### 緩衝開始時

* 呼叫 `trackEvent(BufferStart);`

### 緩衝結束時

* 呼叫 `trackEvent(BufferComplete);`

>[!TIP]
>
>播放頭位置是設定和設定代碼的一部分。 如需詳細資訊，請 `getCurrentPlayheadTime`參閱 [概述：一般實施指引。](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## 實作 {#implement}

1. **初始追蹤設定 -** 識別使用者何時觸發播放意圖 (使用者點按播放和/或自動播放已開啟)，然後使用媒體資訊建立 `MediaObject` 例項，以設定內容名稱、內容 ID、內容長度和資料流類型。

   **`MediaObject`參考：**

   | 變數名稱 | 說明 | 必要 |
   |---|---|---|
   | `name` | 內容名稱 | 是 |
   | `mediaid` | 內容唯一識別碼 | 是 |
   | `length` | 內容長度 | 是 |
   | `streamType` | 資料流類型 | 是 |
   | `mediaType` | 媒體類型 (音效或視訊內容) | 是 |

   **`StreamType`常數：**

   | 常數名稱 | 說明 |
   |---|---|
   | `VOD` | 隨選視訊的資料流類型。 |
   | `LIVE` | Live 內容的資料流類型。 |
   | `LINEAR` | Linear 內容的資料流類型。 |
   | `AOD` | 隨選音效的資料流類型 |
   | `AUDIOBOOK` | 有聲書的資料流類型 |
   | `PODCAST` | 播客的資料流類型 |

   **`MediaType`常數：**

   | 常數名稱 | 說明 |
   |---|---|
   | `Audio` | 音效資料流的媒體類型。 |
   | `Video` | 視訊資料流的媒體類型。 |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **附加中繼資料 -** 可選擇透過內容資料變數，將標準和/或自訂中繼資料物件附加到追蹤工作階段。

   * **標準中繼資料 -**

      >[!NOTE]
      >
      >將標準中繼資料物件附加至媒體物件是選擇性的。

      在媒體心率物件上，實例化標準中繼資料物件、填入必要的變數，然後設定中繼資料物件。

      請在此處參閱完整的中繼資料清單: [音效和視訊參數.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **自訂中繼資料 -** 為自訂變數建立變數物件，並為此內容填入資料。

1. **追蹤開始播放的意圖 -** 若要開始追蹤工作階段，請呼叫媒體心率例項上的 `trackSessionStart`。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 追蹤使用者的播放意圖，而非播放的開始。 此 API 用來載入資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **追蹤實際的播放開始 -**&#x200B;找出來自媒體播放器的播放開始 (畫面上產生內容的第一個影格) 事件，並呼叫 `trackPlay`。

1. **追蹤播放完成 -** 識別來自媒體播放器的播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`。

1. **追蹤工作階段結尾 -** 識別來自媒體播放器的取消載入/關閉播放 (使用者關閉內容及/或內容已完成並取消載入) 事件，並呼叫 `trackSessionEnd`。

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 標示追蹤工作階段的結束。 如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **追蹤所有可能的暫停情況 -** 識別來自媒體播放器的暫停事件，並呼叫 `trackPause`。

   **暫停情況 -** 識別「播放器」會暫停的情況，並請務必正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原內容。

1. 識別來自播放器的播放和/或來自暫停的恢復事件，並呼叫 `trackPlay`。

   >[!TIP]
   >
   >這可能是步驟4中使用的相同事件來源。 Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. 從媒體播放器上聽取播放搜尋事件。在搜尋開始事件通知上使用 `SeekStart` 事件追蹤搜尋。
1. 在來自媒體播放器的搜尋完成通知上，使用 `SeekComplete` 事件來追蹤搜尋的結尾.
1. 接聽來自媒體播放器的播放緩衝事件，並在緩衝開始事件通知時使用 `BufferStart` 事件追蹤緩衝。
1. 在來自媒體播放器的緩衝完成通知上，使用 `BufferComplete` 事件來追蹤緩衝的結尾。

請參閱下列平台專屬主題中每個步驟的範例，並查看 SDK 包含的範例播放器。

如需播放追蹤的簡單範例，請參閱 HTML5 播放器中 JavaScript 2.x SDK 的使用。

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>, 
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## 驗證 {#validate}

如需驗證實作的詳細資訊，請參閱驗 [證。](/help/sdk-implement/validation/validation-overview.md)

