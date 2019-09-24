---
seo-title: 設定 iOS
title: 設定 iOS
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 設定 iOS{#set-up-ios}

## 必備條件

* **取得Media SDK的有效設定參**&#x200B;數在您設定分析帳戶後，這些參數可向Adobe代表取得。
* **在您的應用程式中實作** iOS適用的ADBMobile如需Adobe Mobile SDK檔案的詳細資訊，請參閱 [Experience cloud解決方案適用的iOS SDK 4.x。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >從iOS 9開始，Apple推出了一項稱為App Transport Security(ATS)的功能。 此功能可確保您的應用程式僅使用符合產業標準的通訊協定和密碼，進而提升網路安全。此為預設啟用功能，但您可透過設定選項自行選擇是否使用 ATS。如需ATS的詳細資訊，請參閱 [App Transport Security。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **在您的媒體播放器中提供下列功能:**

   * _訂閱播放器事件專用的 API_ - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * _提供播放器資訊的 API_ - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Media SDK 新增至專案。

   1. 驗證 `libs` 目錄中存在下列軟體元件:

      * `ADBMediaHeartbeat.h`: 用於 iOS 心率追蹤 API 的 Objective-C 標題檔案。
      * `ADBMediaHeartbeatConfig.h`: SDK 設定的 Objective-C 標題檔案。
      * `MediaSDK.a`: 已啟用 bitcode 的大型程式庫，其中包含 iOS 裝置 (armv7、armv7s、arm64) 和模擬器 (i386 和 x86_64) 適用的程式庫組建。

         當預期目標為 iOS 應用程式時，應連結此二進位檔。

      * `MediaSDK_TV.a`: 已啟用 bitcode 的大型程式庫，其中包含新 Apple TV 裝置 (arm64) 和模擬器 (x86_64) 適用的程式庫組建。

         當預期目標為 Apple TV (tvOS) 應用程式時，應該連結此程式庫。
   1. 將程式庫新增至專案:

      1. 啟動 Xcode IDE 並開啟您的應用程式。
      1. 在&#x200B;**[!UICONTROL 專案導覽器]**&#x200B;中，拖曳 `libs` 目錄，並將它放置在您的專案下。

      1. 確保已選取&#x200B;**[!UICONTROL 若需要則複製項目]**&#x200B;核取方塊、已選取&#x200B;**[!UICONTROL 建立群組]，並且未選取**&#x200B;新增至目標]中的任何核取方塊。**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Click **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. 在&#x200B;**[!UICONTROL 「一般」]**&#x200B;標籤的&#x200B;**[!UICONTROL 「連結架構」]**&#x200B;和&#x200B;**[!UICONTROL 「程式庫」]**&#x200B;區段中，連結所需的架構和程式庫。

         **iOS 應用程式目標:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV (tvOS) 目標:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. 驗證應用程式可建置而不會發生錯誤。




1. 匯入資料庫。

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   本節可協助您瞭解 `MediaHeartbeat` 設定參數，以及在您的 `MediaHeartbeat` 例項上設定正確的設定值以提高追蹤準確率。

   以下示範 `ADBMediaHeartbeatConfig` 初始化:

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. 此例項將用於下列所有追蹤事件。

## 在 iOS 中從 1.x 版移轉至 2.x 版 {#migrate-to-two-x}

在 2.x 版中，所有公用方法皆已整合至 `ADBMediaHeartbeat` 類別，讓開發人員更容易操作。所有設定皆已整合至 `ADBMediaHeartbeatConfig` 類別。

For more information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## 設定 tvOS 的原生應用程式

隨著新 Apple TV 的推出，您現在可以建立應用程式以在原生 tvOS 環境中執行。在 iOS 提供的數個架構中，您可以使用任一架構來建立單純的原生應用程式，或可以使用 XML 範本和 JavaScript 來建立您的應用程式。從 MediaSDK 2.0 版開始，已對 tvOS 提供支援。For more information about tvOS, see [tvOS Developer site.](https://developer.apple.com/tvos/documentation/)

在您的 Xcode 專案中執行以下步驟。本指南的編寫是假設您的專案具有的一個目標為以 tvOS 為目標的 Apple TV 應用程式:

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. 在 tvOS 應用程式目標的&#x200B;**[!UICONTROL 「建置階段」]**&#x200B;標籤中，展開&#x200B;**[!UICONTROL 「連結二進位檔與程式庫」]**&#x200B;區段，並新增下列程式庫:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

