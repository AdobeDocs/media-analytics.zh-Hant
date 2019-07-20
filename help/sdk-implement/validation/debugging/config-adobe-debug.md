---
seo-title: 設定 Adobe Debug
title: 設定 Adobe Debug
uuid: e416458d-f23 c-41ce-8d99-fa5076 c455 f0
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# 設定 Adobe Debug{#configure-adobe-debug}

## 存取 Adobe Debug {#section_AF81E7AD331E41FFA371AB9DA924BFBB}

若要存取 Adobe Debug:

1. Go to [Experience Cloud](https://www.marketing.adobe.com) and create a new Adobe Experience Cloud user.

   >[!TIP]
   >
   >此登入不與您用來登入Adobe Analytics的使用者名稱/密碼相同。

1. 擁有 Experience Cloud 帳戶後，請聯絡 Adobe 代表索取 Adobe Debug 存取權限。
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   支援該工具的瀏覽器包括:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 9-11 版

建議的瀏覽器是最新版本的 Chrome 和 Firefox。

## 除錯代理 {#section_8D3493B8426B46DEB9CD7E2ABD785D66}

下載並設定除錯代理程式：

1. Download the Debug Proxy app at [App Downloads.](https://debug.adobe.com/#/downloads)

   支援的作業系統包括:
   * OS X 10.7 64 位元或更新版本
   * Windows 7.1 64 位元或更新版本
   ![](assets/debug-proxy-app.png)

1. 除錯代理伺服器會在本機電腦上執行並透過連接埠 33284 通訊，同時也會設定為系統代理。

   您可能需要根據 OS 和瀏覽器調整瀏覽器設定。

## 下載 SSL 憑證並安裝在桌上型電腦或應用程式上 {#section_2F9547E301CB413299A67BD59AFBEE0D}

首次執行 Adobe Debug 時，系統會產生唯一的 SSL 憑證。如果您的桌上型電腦和/或應用程式支援 HTTPS 流量，便需要下載及安裝我們的 SSL 憑證。

下載並安裝SSL憑證：

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. 匯入憑證

   **Mac OS**
   1. 連按兩下根 CA 憑證，以在鑰匙圈存取中開啟。
   1. 根 CA 憑證會出現在「登入」中。
   1. 將根 CA 憑證移動 (拖曳) 到「系統」。
   1. 您必須將憑證複製到「系統」，確保獲得所有使用者和本機系統程序信任。
   1. 開啟根 CA 憑證、展開「信任」、選取「必須信任」，然後儲存變更。
   **Windows**
   1. 完成下列其中一項程序:

      * [將憑證新增到本機電腦的「受信任的根憑證授權單位」存放區](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1.對於Firefox，請完成「在Mozilla Firefox中安裝根憑證」程序。](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    You might need to quit and reopen Firefox to see the change.
    
    ** iOS裝置**
    1。按一下**[！UICOHTROL設定應用程式]****&gt;****[！UICOHTROL Wifi設定]**。
    
    1. 在Safari中，前往[除錯]。](https://proxy.debug.adobe.com/ssl)
    
    Safari will prompt you to install the SSL certificate.

## 為行動裝置安裝 SSL 憑證 {#section_F2A3336F482C43E2ABEA742AD5CCACCA}

如果您的 Adobe Debug 遺失 HTTPS 呼叫，就必須在行動裝置上安裝 Adobe Debug 的 SSL 憑證。

### iOS 應用程式

若要在 iOS 裝置上安裝 SSL 憑證:

1. On your laptop, turn on the Debug Proxy, and go to [Adobe Debug.](https://debug.adobe.com)
1. 在 iOS 裝置上完成以下步驟:
   1. 將裝置切換為飛航模式。
   1. 選取筆記型電腦使用的 Wi-Fi 訊號。
   1. 在筆記型電腦上，手動設定除錯代理應用程式顯示的 IP 和連接埠。
   1. 開啟 Apple Safari 瀏覽器視窗。
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. 下載及安裝 SSL 憑證。

1. 在筆記型電腦上啟動 Adobe Debug 工作階段。
1. 開始在 iOS 裝置上進行測試。

### Android

若要在 Android 裝置上安裝 SSL 憑證:

1. On your laptop turn on the Debug Proxy and go to [Adobe Debug.](https://debug.adobe.com)
1. 在 Android 裝置上完成以下步驟:
   1. 將裝置設定為飛航模式。
   1. 選取筆記型電腦使用的 Wi-Fi 訊號。
   1. 在筆記型電腦上，手動設定除錯代理應用程式顯示的 IP 和連接埠。
   1. 開啟瀏覽器視窗。
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. 下載及安裝 SSL 憑證。

1. 在筆記型電腦上啟動 Adobe Debug 工作階段。
1. 開始在 Android 裝置上進行測試。

