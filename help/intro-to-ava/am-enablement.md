---
title: 什麼是Adobe Audience Manager啟用？
description: 瞭解如何將應用程式動作連結至媒體追蹤資料，而不需要額外的處理規則和自訂變數。
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 93%

---


# 啟用 Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM) 是一款資料管理平台 (DMP)，能協助您彙集對象資料資產、簡化網站訪客之商業相關資訊的收集、建立可行銷區段，以及將目標廣告和內容提供給合適的對象。

有了 AAM，您不必再侷限於資料賣方、交換或需求端平台。此外，AAM 也無從得知合作夥伴的資料資產。AAM 提供存取多種資料來源的功能，數位發行者將能使用多樣化的第三方資料和我們的私人資料協作。若要深入瞭解 AAM，請參閱 AAM 文件 [Audience Manager 產品文件](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)。

**VA 到 AAM 資料傳輸 -** 針對視訊內容和視訊廣告，透過解決方案 (保留) 變數收集而來的量度和中繼資料能自動傳送給 AAM。資料傳輸可在所有平台上進行，包括桌上型電腦、行動裝置及 OTT。若要啟用伺服器端資料傳輸，您需要聯絡 Adobe Client Care 申請啟用這項摘要。

>[!IMPORTANT]
>
>為了將資料順暢地傳輸到 AAM，您應使用最新版本的 Media SDK 程式庫。

同盟資料完全支援將資料共用到 AAM。請與 Adobe 團隊合作確認同盟資料設定。

## OTT / AAM 方法 {#ott-aam-methods}

您可以使用這些方法來傳送訊號，並從 Audience Manager 擷取訪客區段:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   傳回最近取得的訪客描述檔。若尚未提交任何訊號，則傳回空白物件。

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   傳回最近取得的訪客描述檔。若尚未提交任何訊號，則傳回空白物件。

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   傳回目前的 DPUUID。

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   設定 DPID 和 DPUUID。若已設定 DPID 和 DPUUID，則會與各訊號一併傳送。

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   傳送具特徵的訊號至對象管理。

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   傳回最近取得的訪客描述檔。若尚未提交任何訊號，則傳回空白物件。

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   傳回最近取得的訪客描述檔。若尚未提交任何訊號，則傳回空白物件。

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   傳回目前的 DPUUID。

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   設定 DPID 和 DPUUID。若已設定 DPID 和 DPUUID，則會與各訊號一併傳送。

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   傳送具特徵的訊號至對象管理。

   ```js
   ADBMobile().audienceSubmitSignal()
   ```
