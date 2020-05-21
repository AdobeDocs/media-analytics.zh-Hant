---
title: 設定 Android
description: 適用於 Android 實施的 Media SDK 應用程式設定。
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 92%

---


# 設定 Android{#set-up-android}

>[!IMPORTANT]
>
>在2021年8月31日終止對第4版行動SDK的支援後，Adobe也將終止對iOS和Android專用Media Analytics SDK的支援。  如需詳細資訊，請 [參閱「媒體分析SDK終止支援常見問答」](/help/sdk-implement/end-of-support-faqs.md)。


## 必備條件

* **取得適用於 Media SDK 的有效設定參數**
在您設定分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的應用程式實作 Android 適用的 ADBMobile**
如需 Adobe Mobile SDK 文件的詳細資訊，請參閱 [Experience Cloud 解決方案適用的 Android SDK 4.x](https://docs.adobe.com/content/help/zh-Hant/mobile-services/android/overview.html)。

* **在您的媒體播放器中提供下列功能：**
   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等詳細內容。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK 新增至專案。

   1. 展開 Android 壓縮檔案 (例如 `MediaSDK-android-v2.*.zip`)。
   1. 驗證 `MediaSDK.jar` 目錄中存在 `libs/` 檔案.

   1. 將程式庫新增至專案。

      **IntelliJ IDEA：**

      1. 在&#x200B;**[!UICONTROL 「專案導覽」]**&#x200B;面板中，以滑鼠右鍵按一下專案。
      1. 選取&#x200B;**[!UICONTROL 「開啟模組設定」]**。
      1. 在&#x200B;**[!UICONTROL 「專案設定」]**&#x200B;下，選取&#x200B;**[!UICONTROL 「資料庫」]**。

      1. 按一下 **[!UICONTROL +]** 新增新程式庫。
      1. 選取&#x200B;**[!UICONTROL 「Java」]** 並導覽至 `MediaSDK.jar` 檔案。

      1. 選取您計劃使用行動程式庫所在的模組。
      1. 按一下&#x200B;**[!UICONTROL 「套用」]**，然後按&#x200B;**[!UICONTROL 「確定」]**，關閉「模組設定」視窗。
      **Eclipse：**

      1. 在 Eclipse IDE 中，用滑鼠右鍵按一下專案名稱。
      1. 按一下「**[!UICONTROL 建立路徑]** > **[!UICONTROL 新增外部封存檔]**」。
      1. 選擇 `MediaSDK.jar`.
      1. 按一下&#x200B;**[!UICONTROL 「開啟」]**。
      1. 再次以滑鼠右鍵按一下專案，然後按一下「**[!UICONTROL 組建路徑]** > **[!UICONTROL 設定組建路徑]**」。
      1. 依序按一下&#x200B;**[!UICONTROL 「順序」]**&#x200B;和&#x200B;**[!UICONTROL 「匯出」]**&#x200B;標籤。

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

使用 Media SDK 的應用程式需要下列權限，才能在追蹤呼叫中傳送資料：

* `INTERNET`
* `ACCESS_NETWORK_STATE`

若要新增這些權限，請在應用程式專案目錄裡的 `AndroidManifest.xml` 檔案中加入下列各行:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**在 Android 中從 1.x 版移轉至 2.x 版**

在 2.x 版中，所有公用方法皆已整合至 `com.adobe.primetime.va.simple.MediaHeartbeat` 類別，讓開發人員更容易操作。此外，所有的設定現已整合至 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 類別。

如需有關從 1.x 移轉至 2.x 的詳細資訊，請參閱 [mig-1x-2x-overview.md](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)。
