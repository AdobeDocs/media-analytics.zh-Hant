---
title: 設定 Android
description: 適用於 Android 實施的 Media SDK 應用程式設定。
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# 設定 Android{#set-up-android}

>[!IMPORTANT]
>
>自2020年10月起，Adobe將停止支援第4版Mobile SDK和Android專用的獨立Media Analytics SDK。 您可以繼續下載並使用第4版SDK，但客戶服務支援和論壇存取權將會終止。 您應移轉至Android專用的Adobe Experience Platform(AEP)SDK。 AEP Mobile SDK（先前稱為v5）將獨家支援Adobe Experience Cloud的功能和功能。 如需此變更的詳細資訊，請參 [閱第4版行動SDK支援終止常見問答](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)。 建議您移轉至新的AEP Mobile SDK。
移轉至AEP Mobile SDK後，您必須實作Analytics Launch擴充功能和Media Analytics Launch擴充功能，以啟用Adobe Analytics for Audio和Video。 如需移轉至新AEP Mobile SDK的詳細資訊，請參 [閱從獨立媒體SDK移轉至Adobe Launch ](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)


## 必備條件


* **取得適用於 Media SDK 的有效設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的應用程式實作 Android 適用的 ADBMobile**
如需 Adobe Mobile SDK 文件的詳細資訊，請參閱 [Experience Cloud 解決方案適用的 Android SDK 4.x](https://docs.adobe.com/content/help/zh-Hant/mobile-services/android/overview.html)。

* **在您的媒體播放器中提供下列功能:**
   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK 新增至專案。

   1. 展開 Android 壓縮檔案 (例如 `MediaSDK-android-v2.*.zip`)。
   1. 驗證 `MediaSDK.jar` 目錄中存在 `libs/` 檔案.

   1. 將程式庫新增至專案。

      **IntelliJ IDEA:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. 選擇 **[!UICONTROL Open Module Settings]**.
      1. 在下 **[!UICONTROL Project Settings]**&#x200B;面，選擇 **[!UICONTROL Libraries]**。

      1. Click **[!UICONTROL +]** to add a new library.
      1. Select **[!UICONTROL Java]** and navigate to the `MediaSDK.jar` file.

      1. 選取您計劃使用行動程式庫所在的模組。
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. 在 Eclipse IDE 中，用滑鼠右鍵按一下專案名稱。
      1. 按一下  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. 選擇 `MediaSDK.jar`.
      1. 按一下 **[!UICONTROL Open]**.
      1. 再次以滑鼠右鍵按一下專案，然後按一 **[!UICONTROL Build Path]** 下> **[!UICONTROL Configure Build Path]** 。
      1. 按一下 **[!UICONTROL Order]** 和標 **[!UICONTROL Export]** 簽。

      1. 確認已選取 `MediaSDK.jar` 檔案。


1. 匯入資料庫。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. 建立 `MediaHeartbeatConfig` 例項。

   以下示範 `MediaHeartbeatConfig` 初始化:

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. 實施 `MediaHeartbeatDelegate` 介面。

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. 建立 `MediaHeartbeat` 例項。

   合併使用 `MediaHeartbeatConfig` 例項和 `MediaHertbeatDelegate` 例項，以建立 `MediaHeartbeat` 例項。

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >請確保您的 `MediaHeartbeat` 例項可供存取，並且&#x200B;*不會在工作階段結束前遭到取消配置*。此例項將用於下列所有追蹤事件。

**新增應用程式權限**

使用 Media SDK 的應用程式需要下列權限，才能在追蹤呼叫中傳送資料:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

若要新增這些權限，請在應用程式專案目錄裡的 `AndroidManifest.xml` 檔案中加入下列各行:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**在 Android 中從 1.x 版移轉至 2.x 版**

在 2.x 版中，所有公用方法皆已整合至 `com.adobe.primetime.va.simple.MediaHeartbeat` 類別，讓開發人員更容易操作。此外，所有的設定現已整合至 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 類別。

如需有關從 1.x 移轉至 2.x 的詳細資訊，請參閱 [mig-1x-2x-overview.md](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)。
