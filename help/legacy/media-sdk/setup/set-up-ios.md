---
title: 如何設定 iOS 上的 Media SDK
description: 請依照這些步驟在 iOS 上設定 Media SDK 應用程式。
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 94%

---

# 設定 iOS{#set-up-ios}

瞭解如何為iOS裝置設定串流媒體收集附加元件。

>[!IMPORTANT]
>
>我們於 2021 年 8 月 31 日停止支援第 4 版 Mobile SDK 後，Adobe 也將停止支援 Media Analytics SDK iOS 版和 Android 版。如需詳細資訊，請參閱 [Media Analytics SDK 支援終止常見問題集](/help/additional-resources/end-of-support-faqs.md)。

## 先決條件

* **取得適用於 Media SDK 的有效設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的應用程式實作 iOS 適用的 ADBMobile**
如需 Adobe Mobile SDK 文件的詳細資訊，請參閱 [Experience Cloud 解決方案適用的 iOS SDK 4.x](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=zh-Hant)。

  >[!IMPORTANT]
  >
  >Apple 自 iOS 9 起推出 App Transport Security (ATS) 功能。此功能可確保您的應用程式僅使用符合產業標準的通訊協定和密碼，進而提升網路安全。此功能預設為已啟用，但您可透過設定選項自行選擇是否使用 ATS。如需 ATS 的詳細資訊，請參閱 [App Transport Security](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=zh-Hant)。

* **在您的媒體播放器中提供下列功能：**

   * _訂閱播放器事件專用的 API_ - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * _提供播放器資訊的 API_ - 此資訊包含媒體名稱和播放點位置等詳細內容。

## SDK 實作

>[!IMPORTANT]
>
>自 2.3.0 版起，SDK 會透過 XCFramework 發佈。
>
>SDK 2.3.0 版需搭配 Xcode 12.0 以上版本，以及 Cocoapod 1.10.0 以上版本 (如果適用)。

* 只要提到二進位程式庫檔案，就應改用其 XCFramework 加以取代：
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* 如果在專案中手動新增 Adobe XCFramework，請確定其非內嵌型態。

1. 將[下載的](/help/getting-started/download-sdks.md) Media SDK 新增至專案。

   1. 驗證 `libs` 目錄中存在下列軟體元件：

      * `ADBMediaHeartbeat.h`：用於 iOS 心率追蹤 API 的 Objective-C 標題檔案。
      * `ADBMediaHeartbeatConfig.h`：SDK 設定的 Objective-C 標題檔案。
      * `MediaSDK.a`：已啟用 bitcode 的大型程式庫，其中包含 iOS 裝置 (armv7、armv7s、arm64) 和模擬器 (i386 和 x86_64) 適用的程式庫組建。

        當預期目標為 iOS 應用程式時，應連結此二進位檔。

      * `MediaSDK_TV.a`：已啟用 bitcode 的大型程式庫，其中包含新 Apple TV 裝置 (arm64) 和模擬器 (x86_64) 適用的程式庫組建。

        當預期目標為 Apple TV (tvOS) 應用程式時，應該連結此程式庫。

   1. 將程式庫新增至專案：

      1. 啟動 Xcode IDE 並開啟您的應用程式。
      1. 在&#x200B;**[!UICONTROL 「專案導覽器」]**&#x200B;中，拖曳 `libs` 目錄，並將它放置在您的專案下。

      1. 確保已選取&#x200B;**[!UICONTROL 「若需要則複製項目」]**&#x200B;核取方塊、已選取&#x200B;**[!UICONTROL 「建立群組」]**，並且未選取&#x200B;**[!UICONTROL 「新增至目標」]**&#x200B;中的任何核取方塊。

      ![選擇選項](assets/choose-options_ios.png)

      1. 按一下&#x200B;**[!UICONTROL 「完成」]**。
      1. 在&#x200B;**[!UICONTROL 「專案導覽器」]**&#x200B;中，選取您的應用程式並選取您的目標。
      1. 在&#x200B;**[!UICONTROL 「一般」]**&#x200B;標籤的&#x200B;**[!UICONTROL 「連結架構」]**&#x200B;和&#x200B;**[!UICONTROL 「程式庫」]**&#x200B;區段中，連結所需的架構和程式庫。

         **iOS 應用程式目標：**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Apple TV (tvOS) 目標：**

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

1. 建立 `ADBMediaHeartbeatConfig` 例項。

   本節可協助您瞭解 `MediaHeartbeat` 設定參數，以及在您的 `MediaHeartbeat` 例項上設定正確的設定值以提高追蹤準確率。

   以下示範 `ADBMediaHeartbeatConfig` 初始化：

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

1. 實作 `ADBMediaHeartbeatDelegate` 通訊協定。

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

1. 使用 `ADBMediaHeartBeatConfig` 和 `ADBMediaHeartBeatDelegate` 來建立 `ADBMediaHeartbeat` 例項。

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >請確保您的 `ADBMediaHeartbeat` 例項可供存取，並且&#x200B;*不會在工作階段結束前遭到取消配置*。此例項將用於下列所有追蹤事件。

## 在 iOS 中從 1.x 版移轉至 2.x 版 {#migrate-to-two-x}

在 2.x 版中，所有公用方法皆已整合至 `ADBMediaHeartbeat` 類別，讓開發人員更容易操作。所有設定皆已整合至 `ADBMediaHeartbeatConfig` 類別。

如需有關從 1.x 移轉至 2.x 的資訊，請參閱舊版實作文件。

## 設定 tvOS 的原生應用程式

隨著新 Apple TV 的推出，您現在可以建立應用程式以在原生 tvOS 環境中執行。在 iOS 提供的數個架構中，您可以使用任一架構來建立單純的原生應用程式，或可以使用 XML 範本和 JavaScript 來建立您的應用程式。從 MediaSDK 2.0 版開始，已對 tvOS 提供支援。如需 tvOS 的詳細資訊，請參閱 [tvOS 開發人員網站](https://developer.apple.com/tvos/)。

在您的 Xcode 專案中執行以下步驟。本指南的編寫內容，是假設您的專案具有的一個目標為以 tvOS 為目標的 Apple TV 應用程式：

1. 將`VideoHeartbeat_TV.a`程式庫檔案拖曳至專案的`lib`資料夾。

1. 在tvOS應用程式目標的&#x200B;**[!UICONTROL 建置階段]**&#x200B;標籤中，展開&#x200B;**[!UICONTROL 連結二進位檔與資料庫]**&#x200B;區段，然後新增下列資料庫：

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
