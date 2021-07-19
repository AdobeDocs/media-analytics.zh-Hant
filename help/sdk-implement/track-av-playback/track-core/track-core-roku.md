---
title: 了解如何在Roku上追蹤核心播放
description: 了解如何在Roku上使用Media SDK實作核心追蹤。
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 97%

---

# 在 Roku 上追蹤核心播放{#track-core-playback-on-roku}

本文件涵蓋 SDK 2.x 版中的追蹤。

>[!IMPORTANT]
>若您正在實作 SDK 1.x 版，您可以在此處下載 1.x 開發人員指南: [下載 SDK](/help/sdk-implement/download-sdks.md)

1. **初始追蹤設定**

   識別使用者何時觸發播放的意圖 (使用者點擊「播放」及/或開啟自動播放) 並建立 `MediaObject` 例項。

   **`MediaObject`參考資料:**

   | 變數名稱 | 說明 | 必填 |
   | --- | --- | :---: |
   | `name` | 視訊名稱 | 是 |
   | `mediaid` | 視訊唯一識別碼 | 是 |
   | `length` | 視訊長度 | 是 |
   | `streamType` | 資料流類型 (請參閱下列 _StreamType 常數_) | 是 |
   | `mediaType` | 媒體類型 (請參閱下列 _MediaType 常數_) | 是 |

   **`StreamType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | 隨選視訊的資料流類型。 |
   | `MEDIA_STREAM_TYPE_LIVE` | LIVE 內容的資料流類型。 |
   | `MEDIA_STREAM_TYPE_LINEAR` | LINEAR 內容的資料流類型。 |
   | `MEDIA_STREAM_TYPE_AOD` | 隨選音效的資料流類型 |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | 有聲書的資料流類型 |
   | `MEDIA_STREAM_TYPE_PODCAST` | 播客的資料流類型 |

   **`MediaType`常數:**

   | 常數名稱 | 說明 |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | 音效資料流的媒體類型。 |
   | `MEDIA_STREAM_TYPE_VIDEO` | 視訊資料流的媒體類型。 |

   **為含有 VOD 內容的視訊建立媒體資訊物件:**

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

   **為含有 AOD 內容的視訊建立媒體資訊物件:**

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

   可選擇透過內容資料變數，將標準和/或自訂中繼資料物件附加到追蹤工作階段。

   * **標準中繼資料**

      [在 Roku 上實作標準中繼資料](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >將標準視訊中繼資料物件附加到媒體物件為選用。

   * **自訂中繼資料**

      為自訂變數建立變數物件，並為此視訊填入資料。例如:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **追蹤開始播放的意圖**

   若要開始追蹤媒體工作階段，請呼叫媒體心率例項上的 `trackSessionStart`:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >秒數值是您在步驟 2 建立的自訂視訊中繼資料物件名稱。

   >[!IMPORTANT]
   >`trackSessionStart` 會追蹤使用者的播放意圖，而非播放的開始。此 API 用來載入視訊資料/中繼資料，以及估計開始 QoS 量度所需的時間 (`trackSessionStart` 與 `trackPlay` 之間的時間)。

   >[!NOTE]
   >若您未使用自訂視訊中繼資料，只要對 `trackSessionStart` 中的 `data` 引數傳送空白物件即可，如上方 iOS 範例中的備註行所示。

1. **追蹤實際的播放開始**

   識別來自視訊播放器的視訊播放開始 (在畫面上轉譯了視訊的第一個時間格) 事件，並呼叫 `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **追蹤播放完成**

   識別來自視訊播放器的視訊播放完成 (使用者已觀看內容至結尾) 事件，並呼叫 `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **追蹤工作階段結尾**

   識別來自視訊播放器的視訊播放卸載/關閉 (使用者關閉視訊和/或視訊完成及卸載) 事件，並呼叫 `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` 會標記視訊追蹤工作階段的結尾。如果成功觀看工作階段至完成 (使用者觀看了內容至結尾)，請確定在 `trackComplete` 之前呼叫 `trackSessionEnd`。除了新視訊追蹤工作階段的 `trackSessionStart` 外，在 `trackSessionEnd` 之後會忽略任何其他 `track*` API 呼叫。

1. **追蹤所有可能的暫停情況**

   識別來自視訊播放器視訊暫停的事件，並呼叫 `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **暫停情況**

   識別視訊播放器將暫停的任何案例，並確定正確呼叫 `trackPause`。以下情形都要求應用程式呼叫 `trackPause()`:

   * 使用者明確在應用程式中點擊暫停。
   * 播放器自行進入「暫停」狀態。
   * (*行動應用程式*) - 使用者讓應用程式進入背景，但您希望應用程式保持工作階段開啟。
   * (*行動應用程式*) - 發生任何類型的系統中斷，導致應用程式進入背景。例如，使用者接聽電話、或發生來自另一個應用程式的彈出視窗，但您希望應用程式維持工作階段進行中，讓使用者能夠從中斷點復原影片。

1. 識別來自播放器的視訊播放和/或來自暫停的視訊恢復事件，並呼叫 `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >這可能與在步驟 4 使用的事件來源相同。在視訊播放繼續時，使用後續的 `trackPause()` API 呼叫確保 `trackPlay()` API 呼叫成對。

* 追蹤案例：[沒有廣告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 完整追蹤範例的 Roku SDK 包含範例播放器。
