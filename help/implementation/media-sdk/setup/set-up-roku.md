---
title: 如何設定 Roku 的 Media SDK
description: 請依照這些步驟在 Roku 上設定 Media SDK 應用程式。
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 82%

---

# 設定Roku適用的Mobile SDK v2.x {#set-up-roku}

## 先決條件 {#roku-prerequisites}

* **取得Media Analytics的有效設定參數**

   在您設定媒體分析帳戶後，即可從Adobe代表取得這些參數。
* **在您的媒體播放器中加入下列API**

   * _訂閱播放器事件專用的 API_ - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * _提供播放器資訊的 API_ - 此資訊包含媒體名稱和播放點位置等詳細內容。

適用於Experience Cloud解決方案的Roku SDK 2.x可讓您測量在BrightScript中撰寫的Roku應用程式、透過對象管理運用與收集對象資料，以及透過視訊事件測量視訊參與。

## 行動程式庫/ SDK實作

1. 將[下載的](/help/getting-started/download-sdks.md) Roku 程式庫新增至專案。

   1. `AdobeMobileLibrary-2.*-Roku.zip` 下載檔案包含下列軟體元件：

      * `adbmobile.brs`：此程式庫檔案將會包含在您的 Roku 應用程式來源檔案夾中。

      * `ADBMobileConfig.json`：此元件為根據您應用程式自訂的 SDK 設定檔案。
   1. 新增程式庫檔案和 JSON 設定檔案至您的專案來源。

      用來設定Adobe行動的JSON有一個媒體分析專用的索引鍵，稱為 `mediaHeartbeat`. 這是media analytics設定參數的所屬位置。

      >[!TIP]
      >
      >套件會隨附 `ADBMobileConfig` JSON 檔案範例。如需設定，請聯絡 Adobe 代表。

      例如：

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
          "offlineEnabled":false,
          "lifecycleTimeout":30,
          "batchLimit":50,
          "privacyDefault":"optedin",
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{
        "clientCode":"",
        "timeout":5
      },
      "audienceManager":{
        "server":""
      },
      "acquisition":{
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{
         "server":"example.com",
         "publisher":"sample-publisher",
         "channel":"sample-channel",
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | 設定參數 | 說明 |
      | --- | --- |
      | `server` | 代表後端追蹤端點之 URL 的字串。 |
      | `publisher` | 代表內容發行者唯一識別碼的字串。 |
      | `channel` | 代表內容分送管道之名稱的字串。 |
      | `ssl` | 代表是否應使用 SSL 來追蹤呼叫的布林值。 |
      | `ovp` | 代表視訊播放器提供者之名稱的字串。 |
      | `sdkversion` | 代表應用程式/SDK 目前版本的字串。 |
      | `playerName` | 代表播放器名稱的字串。 |

      >[!IMPORTANT]
      >
      >如果 `mediaHeartbeat` 的設定不正確，媒體模組 (VHL) 會進入錯誤狀態並停止傳送追蹤呼叫。


1. 設定 Experience Cloud 訪客 ID。

   Experience Cloud 訪客 ID 服務提供跨 Experience Cloud 解決方案的通用訪客 ID。視訊事件和其他Marketing Cloud整合需要訪客ID服務。

   確認您的 `ADBMobileConfig` 設定包含 `marketingCloud` 組織 ID。

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Experience Cloud 組織 ID 會唯一識別 Adobe Marketing Cloud 中的每一間客戶公司，並出現以下類似值：`016D5C175213CCA80A490D05@AdobeOrg`。

   >[!IMPORTANT]
   >
   >一定要包含 `@AdobeOrg`。

   完成設定後，即會產生一個 Experience Cloud 訪客 ID，並包含在所有點撃中。其他訪客 ID (例如 `custom` 和 `automatically-generated` ID) 會繼續在每次點撃時一併傳送。

   **Experience Cloud 訪客 ID 服務方法**

   >[!TIP]
   >
   >Experience Cloud 訪客 ID 方法的前置詞為 `visitor`。

   |  方法 | 說明 |
   | --- | --- |
   | `visitorMarketingCloudID` | 從訪客 ID 服務中擷取 Experience Cloud 訪客 ID。 <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | 透過 Experience Cloud 訪客 ID，您可以設定與每個訪客相關聯的額外客戶 ID。訪客 API 可接受同一名訪客具有多個客戶 ID，並透過客戶類型識別碼來區分不同客戶 ID 的範圍。此方法對應至 `setCustomerIDs`。例如：<br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | 用來在 SDK 上設定適用於廣告的 Roku ID (RIDA)例如︰<br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>使用 Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API 取得適用於廣告的 Roku ID (RIDA)。 |
   | `getAllIdentifiers` | 傳回 SDK 儲存的所有識別碼清單，包括分析、訪客、Audience Manager 和客戶識別碼。<br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **其他公用 API**

   **DebugLogging**

   |  方法 | 說明 |
   | --- | --- |
   | `setDebugLogging` | 用於啟用或停用 SDK 的偵錯記錄。<br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | 如果啟用偵錯記錄，則傳回 True。<br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  常數   | 說明 |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | 呼叫 setPrivacyStatus 以選擇加入時要傳遞的常數。<br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | 呼叫 setPrivacyStatus 以選擇退出時要傳遞的常數。<br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  方法 | 說明 |
   | --- | --- |
   | `setPrivacyStatus` | 設定 SDK 上的隱私權狀態。  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | 取得在 SDK 上設定的目前隱私權狀態。  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >確保您每 250 ms 呼叫主事件迴圈中的 `processMessages` 和 `processMediaMessages` 函數，以確保 SDK 傳出 Ping。

   |  方法 | 說明 |
   | --- | --- |
   | `processMessages` | 負責傳遞分析事件至要處理的 SDK。  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | 負責傳遞媒體事件至要處理的 SDK。<br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->