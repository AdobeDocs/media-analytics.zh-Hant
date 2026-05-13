---
title: 什麼是 Adobe Audience Manager 輔助？
description: 了解如何將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# 啟用 Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM) 是一款資料管理平台 (DMP)，能協助您彙集對象資料資產、簡化網站訪客之商業相關資訊的收集、建立可行銷區段，以及將目標廣告和內容提供給合適的對象。

有了 AAM，您不必再侷限於資料賣方、交換或需求端平台。 此外，AAM 也無從得知合作夥伴的資料資產。 AAM 提供存取多種資料來源的功能，數位發行者將能使用多樣化的第三方資料。 若要深入了解 AAM，請參閱 AAM 文件 [Audience Manager 產品文件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=zh-Hant)。

**VA 到 AAM 資料傳輸**：針對視訊內容和視訊廣告，透過解決方案 (保留) 變數收集而來的量度和中繼資料能自動傳送給 AAM。 資料傳輸可在所有平台上進行，包括桌上型電腦、行動裝置及 OTT。 若要啟用伺服器端資料傳輸，您需要連絡 Adobe Client Care 申請啟用這項摘要。

>[!IMPORTANT]
>
>為了將資料順暢地傳輸到 AAM，您應使用最新版本的 Media SDK 程式庫。

同盟資料完全支援將資料共用到 AAM。 請與 Adobe 團隊合作確認同盟資料設定。

## OTT / AAM 方法 {#ott-aam-methods}

您可以使用這些方法來傳送訊號，並從 Audience Manager 擷取訪客區段：

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  傳回最近取得的訪客輪廓。 若尚未提交任何訊號，則傳回空白物件。

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  傳回最近取得的訪客輪廓。 若尚未提交任何訊號，則傳回空白物件。

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  傳回目前的 DPUUID。

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  設定 DPID 和 DPUUID。 若已設定 DPID 和 DPUUID，則會與各訊號一併傳送。

  ```js
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  傳送具特徵的訊號至客群管理。

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
  ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

  傳回最近取得的訪客輪廓。 若尚未提交任何訊號，則傳回空白物件。

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  傳回最近取得的訪客輪廓。 若尚未提交任何訊號，則傳回空白物件。

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  傳回目前的 DPUUID。

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  設定 DPID 和 DPUUID。 若已設定 DPID 和 DPUUID，則會與各訊號一併傳送。

  ```js
  ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
  ```

* `audienceSubmitSignal -`

  傳送具特徵的訊號至客群管理。

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
