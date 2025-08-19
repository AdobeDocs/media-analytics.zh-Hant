---
title: 如何設定 Chromecast 適用的 Media SDK
description: 請依照這些步驟在 Chromecast 上設定 Media SDK 應用程式。
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 97%

---

# 設定 Chromecast 適用的 Mobile SDK v3.x {#set-up-chromecast}

本節說明為Adobe串流媒體服務設定Chromecast安裝的先決條件。

## 先決條件

* **取得有效設定參數**

  設定 Media Analytics 帳戶之後，可以向 Adobe 代表取得這些參數。
* **在您的媒體播放器中包含以下 API**

   * *訂閱播放器事件專用的 API* - 當您的播放器中發生事件時，Media SDK 需要您呼叫一組簡易 API。
   * *提供播放器資訊的 API* - 此資訊包含媒體名稱和播放點位置等詳細內容。

Adobe Mobile Services 提供的新使用者介面，將 Adobe Marketing Cloud 適用於行動應用程式的各項行動行銷功能整合在一起。Mobile 服務起初是提供 Adobe Analytics 和 Adobe Target 解決方案的應用程式分析和定位功能流暢整合。如需詳細資訊，請參閱 [Adobe Mobile Services 文件](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=zh-Hant)。

Experience Cloud 解決方案適用的 Chromecast v3.x Adobe Mobile Library 可讓您測量在 JavaScript 中撰寫的 Chromecast 應用程式、透過客群管理利用和收集客群資料，以及測量視訊參與。

## Mobile Library/SDK 實作

1. 將下載的 Chromecast 程式庫新增至專案。

   1. `AdobeMobileLibrary-Chromecast-[version]` zip 檔案包含下列軟體元件：

      * `adbmobile-chromecast.min.js`：

        此程式庫檔案將會包含在您的 Chromecast 應用程式來源檔案夾中。

      * `ADBMobileConfig` 設定

        此元件為根據您應用程式自訂的 SDK 設定檔案。範例 `ADBMobileConfig` 實作會連同 SDK 一併提供 (位於 `samples/` 下方)。請向 Adobe 代表索取適當設定。

   1. 將程式庫檔案新增至您的 `index.html` 檔案，接著建立 `ADBMobileConfig` 全域變數，方法如下 (用來設定 Adobe Mobile for Media Analytics 的全域變數有一個專用的索引鍵，稱為 `mediaHeartbeat`)：

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
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
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
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
      >如果 `mediaHeartbeat` 的設定不正確，媒體模組會進入錯誤狀態並停止傳送追蹤呼叫。

      適用於 mediaHeartbeat 索引鍵的 ADBMobile 設定參數：

   | 設定參數 | 說明 |
   | --- | --- |
   | `server` | 代表後端追蹤端點之 URL 的字串。 |
   | `publisher` | 代表內容發行者唯一識別碼的字串。 |
   | `channel` | 代表內容分送管道之名稱的字串。 |
   | `ssl` | 代表是否應使用 SSL 來追蹤呼叫的布林值。 |
   | `ovp` | 代表視訊播放器提供者之名稱的字串。 |
   | `sdkversion` | 代表應用程式/SDK 目前版本的字串。 |
   | `playerName` | 代表播放器名稱的字串。 |


1. 設定 Experience Cloud 訪客 ID。

   Experience Cloud 訪客 ID 服務提供跨 Experience Cloud 解決方案的通用訪客 ID。Media Analytics 和其他 Marketing Cloud 整合需要訪客 ID 服務。

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

   | 方法 | 說明 |
   | --- | --- |
   | `getMarketingCloudID()` | 從訪客 ID 服務中擷取 Experience Cloud 訪客 ID。 <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | 透過 Experience Cloud 訪客 ID，您可以設定與每個訪客相關聯的額外客戶 ID。訪客 API 可接受同一名訪客具有多個客戶 ID，並透過客戶類型識別碼來區分不同客戶 ID 的範圍。此方法對應至 JavaScript 資料庫中的 `setCustomerIDs()`。例如：<br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. 如果是追蹤媒體，實作 MediaDelegate 通訊協定

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
