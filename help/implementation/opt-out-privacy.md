---
title: 退出與隱私權說明
description: 了解如何處理選擇加入、選擇退出和隱私權。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 88%

---

# 退出與隱私權{#opt-out-and-privacy}

## 退出/加入 {#opt-out-opt-in}

您可以控制特定裝置上是否允許追蹤活動。

* **行動應用程式 -** VA 資料庫會依照 `AdobeMobile` 資料庫的隱私權和退出設定。若要退出追蹤，必須使用 `AdobeMobile` 資料庫。如需 `AdobeMobile` 資料庫的退出和隱私權設定詳細資訊，請參閱[退出和隱私權設定](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html)。
* **JavaScript/瀏覽器應用程式 -** VA 資料庫會依照 `VisitorAPI` 隱私權和退出設定。若要退出追蹤，您需要從訪客 API 服務退出。如需有關選擇退出和隱私權的進一步資訊，請參閱 [Adobe Experience Platform Identity 服務](https://experienceleague.adobe.com/docs/id-service/using/home.html)。
* **OTT 應用程式 (Chromecast、Roku) -** OTT SDK 提供符合一般資料保護規範 (GDPR) 的 API，讓您將資料收集和傳輸的狀態標幟設為 `opt`，並擷取儲存於本機的身分識別資料。

   >[!NOTE]
   >
   >如果隱私權狀態設為退出，也會停用媒體心率追蹤呼叫。

   您可以使用以下設定控制是否在特定裝置上傳送 Analytics 資料：

   * `privacyDefault` 設定檔案中的 `ADBMobile.json` 設定。這會控制持續使用的初始設定，直到在程式碼中變更為止。

   * `ADBMobile().setPrivacyStatus()` 方法。

      * **選擇退出：**

         * **Chromecast：**

                &quot;
                ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
                &quot;
            
         * **Roku：**

                &quot;
                ADBMobile()。setPrivacyStatus(ADBMobile()。PRIVACY_STATUS_OPT_OUT)
                &quot;
            
            >[!IMPORTANT]
            >
            >當使用者選擇退出追蹤時，應用程式將清除所有保存的裝置資料和 ID，直到使用者重新加入為止。
      * **再次加入：**

         * **Chromecast：**

                &quot;
                ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
                &quot;
            
         * **Roku：**

                &quot;
                ADBMobile()。setPrivacyStatus(ADBMobile()。PRIVACY_STATUS_OPT_IN)
                &quot;
            * **傳回目前設定：**

         * **Chromecast：**

                &quot;
                ADBMobile.config.getPrivacyStatus()
                &quot;
            
         * **Roku：**

                &quot;
                ADBMobile()。getPrivacyStatus()
                &quot;
            使用 `setPrivacyStatus` 變更隱私權設定後，變更為永久有效，直到使用此方法再次變更，或者應用程式解除安裝並重新安裝為止。

## 擷取儲存的識別碼 (OTT 應用程式) {#retrieving-stored-identifiers-ott-apps}

這些資訊有助於從 Roku 應用程式擷取存放在本機的使用者身分識別資料。

>[!IMPORTANT]
>
>擷取所有識別碼的方法會取得已知且由 SDK 保存的所有使用者身分識別資料。您必須在使用者選擇退出&#x200B;**之前**&#x200B;呼叫此方法。

存放在本機的身分識別資料會以 JSON 字串傳回，其中包括：

* 公司內容 - IMS 組織 ID
* 使用者 ID
* Experience Cloud ID (MCID)
* 資料來源 ID (DPID、DPUUID)
* Analytics ID (AVID、AID、VID 以及相關 RSID)
* Audience Manager ID (UUID)

例如：

* **Chromecast：**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku：**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```
