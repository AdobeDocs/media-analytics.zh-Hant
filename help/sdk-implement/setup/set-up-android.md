---
seo-title: 設定 Android
title: 設定 Android
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# 設定 Android{#set-up-android}

## 必備條件

* **取得Media SDK的有效設定參**&#x200B;數在您設定分析帳戶後，這些參數可向Adobe代表取得。
* **在您的應用程式中實作Android適用的ADBMobile**&#x200B;如需Adobe Mobile SDK檔案的詳細資訊，請參閱 [Experience cloud解決方案適用的Android SDK 4.x。](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **在您的媒體播放器中提供下列功能:**
   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK 新增至專案。

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. 將程式庫新增至專案。

      **IntelliJ IDEA:**

      1. 在&#x200B;**[!UICONTROL 「專案導覽」]**&#x200B;面板中，以滑鼠右鍵按一下專案。
      1. 選取&#x200B;**[!UICONTROL 開啟模組設定]**。
      1. 在&#x200B;**[!UICONTROL 專案設定]**&#x200B;下，選取&#x200B;**[!UICONTROL 資料庫]**。

      1. Click **[!UICONTROL +]** to add a new library.
      1. 選取 **[!UICONTROL Java]** 並導覽至 `MediaSDK.jar` 檔案。

      1. 選取您計劃使用行動程式庫所在的模組。
      1. 按一下&#x200B;**[!UICONTROL 「套用」]**，然後按&#x200B;**[!UICONTROL 「確定」]**，關閉「模組設定」視窗。
      **Eclipse:**

      1. 在 Eclipse IDE 中，用滑鼠右鍵按一下專案名稱。
      1. 按一下&#x200B;**[!UICONTROL 建立路徑]** &gt; **[!UICONTROL 新增外部封存檔]**。
      1. 選擇 `MediaSDK.jar`.
      1. 按一下&#x200B;**[!UICONTROL 開啟]**。
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. 依序按一下&#x200B;**[!UICONTROL 「順序」]**&#x200B;和&#x200B;**[!UICONTROL 「匯出」]**&#x200B;標籤。

      1. 確認已選取 `MediaSDK.jar` 檔案。


1. 匯入資料庫。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. 此例項將用於下列所有追蹤事件。

**新增應用程式權限**

使用 Media SDK 的應用程式需要下列權限，才能在追蹤呼叫中傳送資料:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

若要新增這些權限，請在應用程式專案目錄裡的 `AndroidManifest.xml` 檔案中加入下列各行:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**在 Android 中從 1.x 版移轉至 2.x 版**

在 2.x 版中，所有公用方法皆已整合至 `com.adobe.primetime.va.simple.MediaHeartbeat` 類別，讓開發人員更容易操作。此外，所有的設定現已整合至 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 類別。

有關從1.x遷移到2.x的詳細資訊，請參 [閱mig-1x-2x-overview.md。](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
