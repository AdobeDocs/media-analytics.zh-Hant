---
seo-title: 設定 Chromecast
title: 設定 Chromecast
uuid: d664e394-02a2-4985-bad-be1 bcc44 fb2 b
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# 設定 Chromecast{#set-up-chromecast}

## 常見問題解答

_我該使用 Chromecast JavaScript SDK 嗎? 還是說，我可以使用標準 JavaScript SDK 呢?_

基於下列原因，正確答案是「Chromecast」：
* 標準 JS SDK 中的 AppMeasurement 和 VisitorAPI 程式庫未經認證可在 OTT 平台上運作。在 Chromecast JS SDK 中，視訊心率程式庫 (VHL)、Analytics 和 VisitorAPI 均內建於單一、統一且經過 Chromecast 認證的 SDK 中。
* Chromecast SDK 比起標準 JS SDK 更輕量得多。這對 OTT 平台使用的低階硬體非常重要。

## 必備條件

* **取得活動訊號的有效設定參數**&#x200B;這些參數可在您設定媒體分析帳戶後由Adobe代表取得。
* **在您的媒體播放器中提供下列功能:**
   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等等的詳細內容。

Adobe Mobile Services 提供的新使用者介面，將 Adobe Marketing Cloud 適用於行動應用程式的各項行動行銷功能整合在一起。Mobile 服務起初是提供 Adobe Analytics 和 Adobe Target 解決方案的應用程式分析和定位功能流暢整合。Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Experience Cloud 解決方案適用的 Chromecast SDK 2.x 可讓您測量在 JavaScript 中撰寫的 Chromecast 應用程式、透過對象管理利用和收集對象資料，以及透過視訊心率測量視訊參與。

## SDK 實作

1. 將[下載的](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Chromecast 程式庫新增至專案。

   1. `AdobeMobileLibrary-Chromecast-[version]` zip 檔案包含下列軟體元件:

      * `adbmobile-chromecast.min.js`:

         此程式庫檔案將會包含在您的 Chromecast 應用程式來源檔案夾中。

      * `ADBMobileConfig` config

         此元件為根據您應用程式自訂的 SDK 設定檔案。範例 `ADBMobileConfig` 實施會連同 SDK 一併提供 (位於 `samples/` / 下方)。請向 Adobe 代表索取適當設定。
   1. 將程式庫檔案新增至您的 `index.html` 檔案，接著建立 `ADBMobileConfig` 全域變數，方法如下 (用來設定 Adobe Mobile for Heartbeats 的全域變數有一個專用的索引鍵，稱為 `mediaHeartbeat`):

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      適用於 mediaHeartbeat 索引鍵的 ADBMobile 設定參數:
   | 設定參數 | 說明     |
   | --- | --- |
   | `server` | 代表後端追蹤端點之 URL 的字串。 |
   | `publisher` | 代表內容發行者唯一識別碼的字串。 |
   | `channel` | 代表內容分送管道之名稱的字串。 |
   | `ssl` | 代表是否應使用 SSL 來追蹤呼叫的布林值。 |
   | `ovp` | 代表視訊播放器提供者之名稱的字串。 |
   | `sdkversion` | 代表應用程式/SDK 目前版本的字串。 |
   | `playerName` | 代表播放器名稱的字串。 |


1. 設定 Experience Cloud 訪客 ID。

   Experience Cloud 訪客 ID 服務提供跨 Experience Cloud 解決方案的通用訪客 ID。視訊心率和其他 Marketing Cloud 整合需要訪客 ID 服務。

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   完成設定後，即會產生一個 Experience Cloud 訪客 ID，並包含在所有點撃中。Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 訪客 ID 服務方法**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | 方法 | 說明 |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | 透過 Experience Cloud 訪客 ID，您可以設定與每個訪客相關聯的額外客戶 ID。訪客 API 可接受同一名訪客具有多個客戶 ID，並透過客戶類型識別碼來區分不同客戶 ID 的範圍。此方法對應至 JavaScript 資料庫中的 `setCustomerIDs()`。For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

