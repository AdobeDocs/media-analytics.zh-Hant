---
title: 設定 Roku
description: 適用於 Roku 實作的 Media SDK 應用程式設定。
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '577'
ht-degree: 100%

---


# 設定 Roku{#set-up-roku}

## 必備條件

* **取得心率適用的有效設定參數**
在您設定媒體分析帳戶後，即可從 Adobe 代表取得這些參數。
* **在您的媒體播放器中提供下列功能：**
   * _訂閱播放器事件專用的 API_ - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * _提供播放器資訊的 API_ - 此資訊包含媒體名稱和播放點位置等詳細內容。

Adobe Mobile Services 提供的新使用者介面，將 Adobe Marketing Cloud 適用於行動應用程式的各項行動行銷功能整合在一起。Mobile 服務起初是提供 Adobe Analytics 和 Adobe Target 解決方案的應用程式分析和定位功能流暢整合。

如需詳細資訊，請參閱 [Adobe Mobile Services 文件](https://docs.adobe.com/content/help/zh-Hant/mobile-services/using/home.html)。

Experience Cloud 解決方案適用的 Roku SDK 2.x 可讓您測量在 BrightScript 中撰寫的 Roku 應用程式、透過對象管理利用和收集觀眾資料，以及透過視訊心率測量視訊參與。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku 程式庫新增至專案。

   1. `AdobeMobileLibrary-2.*-Roku.zip` 下載檔案包含下列軟體元件：

      * `adbmobile.brs`：此程式庫檔案將會包含在您的 Roku 應用程式來源檔案夾中。

      * `ADBMobileConfig.json`：此元件為根據您應用程式自訂的 SDK 設定檔案。
   1. 新增程式庫檔案和 JSON 設定檔案至您的專案來源。

      用來設定 Adobe Mobile 的 JSON 有一個媒體心率專用的索引鍵，稱為 `mediaHeartbeat`。其集結了多種媒體心率的設定參數。

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
          "ssl":false, 
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
         "ssl":false,
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

   Experience Cloud 訪客 ID 服務提供跨 Experience Cloud 解決方案的通用訪客 ID。視訊心率和其他 Marketing Cloud 整合需要訪客 ID 服務。

   確認您的 `ADBMobileConfig` 設定包含 `marketingCloud` 組織 ID。

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
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

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
