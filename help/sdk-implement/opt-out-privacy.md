---
seo-title: 退出與隱私權
title: 退出與隱私權
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# 退出與隱私權{#opt-out-and-privacy}

## 退出/加入 {#section_zfb_syq_v2b}

您可以控制特定裝置上是否允許追蹤活動。

* **行動應用程式 -** VA 資料庫會依照 `AdobeMobile` 資料庫的隱私權和退出設定。若要退出追蹤，必須使用 `AdobeMobile` 資料庫。如需 `AdobeMobile` 資料庫的退出和隱私權設定詳細資訊，請參閱[退出和隱私權設定](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)。
* **JavaScript/瀏覽器應用程式 -** VA 資料庫會依照 `VisitorAPI` 隱私權和退出設定。若要退出追蹤，您需要從訪客 API 服務退出。For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT Apps(Chromecast, Roku)**`opt` - OTT SDK提供通用資料保護規則(GDPR)適用的API，可讓您設定資料收集和傳輸的狀態標幟，並擷取本機儲存的身分。

   >[!NOTE]
   >
   >如果隱私權狀態設為選擇退出，媒體心率追蹤呼叫也會停用。

   您可以使用以下設定控制是否在特定裝置上傳送 Analytics 資料:

   * The `privacyDefault` setting in the `ADBMobile.json` config file. 這會控制持續使用的初始設定，直到在程式碼中變更為止。

   * 方 `ADBMobile().setPrivacyStatus()` 法。

      * **選擇退出:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >當使用者退出追蹤時，所有持續的裝置資料和ID都會被清除，直到使用者返回為止。

      * **再次加入:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **傳回目前設定:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   使用 `setPrivacyStatus` 變更隱私權設定後，變更為永久有效，直到使用此方法再次變更，或者應用程式解除安裝並重新安裝為止。

## 擷取儲存的識別碼 (OTT 應用程式) {#section_mky_2yq_v2b}

這些資訊有助於從 Roku 應用程式擷取存放在本機的使用者身分識別資料。

>[!IMPORTANT]
>
>擷取所有識別碼的方法會取得SDK已知並持續存在的所有使用者識別碼。 您必須在使用者選擇退出&#x200B;**之前**&#x200B;呼叫此方法。

存放在本機的身分識別資料會以 JSON 字串傳回，其中包括:

* 公司內容 - IMS 組織 ID
* 使用者 ID
* Experience Cloud ID (MCID)
* 資料來源 ID (DPID、DPUUID)
* Analytics ID (AVID、AID、VID 以及相關 RSID)
* Audience Manager ID (UUID)

例如:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

