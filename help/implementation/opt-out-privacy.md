---
title: 選擇退出與隱私權設定
description: 了解如何處理選擇加入、選擇退出和隱私權。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 3fd9ffcb997e1570abb983107e69d183b1c8b311
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# 選擇退出與隱私權設定

當使用者選擇退出追蹤時，串流媒體程式庫會立即停止所有資料收集活動。 不會為該使用者傳送工作階段開始呼叫、心率Ping，以及事件追蹤資料至Adobe資料收集伺服器。

## 選擇退出/選擇加入

選擇退出控制項會依裝置或瀏覽器操作。 尊重使用者同意是實作組織的責任。 如需Adobe隱私權實務的概觀，請參閱[Adobe隱私權中心](https://www.adobe.com/tw/privacy.html)。

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

Web SDK會遵守使用`setConsent`命令設定的同意偏好設定。 當同意設為`"out"`時，Web SDK會停止轉送所有事件（包括串流媒體追蹤呼叫）至Edge Network。 同意狀態會在工作階段之間持續存在於瀏覽器儲存中。

在實作選擇退出之前，請確定您的網頁SDK已設定串流媒體元件。 如需詳細資訊，請參閱[設定網頁SDK](../implementation/edge/web-sdk.md)。

使用Adobe 2.0同意標準將同意設為選擇退出：

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

同意值：

* `"y"`：選擇加入（允許資料收集）
* `"n"`：選擇退出（資料收集已隱藏）
* `"p"`：擱置中（等待使用者決定；在解析之前不會收集任何資料）

若要還原追蹤，請以`"y"`作為`collect.val`值，再次呼叫`setConsent`。

如需其他格式，包括IAB TCF 2.0，請參閱Web SDK檔案中的[setConsent命令](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent)。

>[!TAB iOS]

Adobe Experience Platform Mobile SDK尊重使用`MobileCore.setPrivacyStatus()`設定的隱私權狀態。 將狀態設定為`.optedOut`會隱藏所有AEP擴充功能（包括串流媒體）的所有資料收集。 狀態會在各應用程式工作階段中持續存在。

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

若要還原追蹤，請將隱私權狀態設定回`.optedIn`：

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

如需詳細資訊，請參閱AEP Mobile SDK檔案中的[隱私權與GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)。

>[!TAB Android]

Adobe Experience Platform Mobile SDK尊重使用`MobileCore.setPrivacyStatus()`設定的隱私權狀態。 將狀態設定為`MobilePrivacyStatus.OPT_OUT`會隱藏所有AEP擴充功能（包括串流媒體）的所有資料收集。 狀態會在各應用程式工作階段中持續存在。

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

若要還原追蹤，請將隱私權狀態設定回`MobilePrivacyStatus.OPT_IN`：

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

如需詳細資訊，請參閱AEP Mobile SDK檔案中的[隱私權與GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)。

>[!TAB Roku Edge]

Roku Edge SDK使用`setConsent()`搭配Adobe 2.0同意標準。 將`collect.val`設定為`"n"`會立即停止所有資料收集，包括串流媒體事件。

同意值：

* `"y"`：選擇加入（允許資料收集）
* `"n"`：選擇退出（資料收集已隱藏）
* `"p"`：擱置中（等待使用者決定；在解析之前不會收集任何資料）

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

若要還原追蹤，請將`collect.val`設定為`"y"`並再次呼叫`setConsent()`。

您也可以在SDK初始化時使用`updateConfiguration()`搭配`ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`金鑰設定預設同意值。 如需詳細資訊，請參閱[Roku Edge SDK檔案](https://github.com/adobe/aepsdk-roku)。

>[!TAB Media Edge API]

Media Edge API是伺服器端實作。 SDK層不會自動強制同意 — 您的應用程式必須先檢查使用者同意狀態，才能進行API呼叫並隱藏選擇退出使用者的請求。

對於完整選擇退出，對於選擇退出的使用者，請勿在`/va/v2/sessions`端點（或任何後續事件端點）進行POST：

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

如需詳細資訊，請參閱[Media Edge API參考](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)。

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK JS 3.x程式庫會遵循Adobe訪客API （身分服務）選擇退出狀態。 當使用者選擇退出使用訪客API時，Media SDK會自動抑制所有追蹤呼叫。

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

將`YOUR_ORG_ID@AdobeOrg`取代為您的來自Adobe Admin Console的組織ID。

若要還原追蹤，請將`false`傳遞至`setOptOut()`。

如需詳細資訊，請參閱[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html)。

>[!TAB Chromecast]

Chromecast Media SDK 3.x尊重使用`ADBMobile.config.setPrivacyStatus()`所設定的隱私權狀態。 將狀態設定為`PRIVACY_STATUS_OPT_OUT`會隱藏所有資料集合。

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

若要還原追蹤，請將狀態設回opted in：

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

您也可以在您的`ADBMobileConfig`物件中，於SDK初始化時設定預設隱私權狀態：

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

Roku 2.x SDK尊重使用`setPrivacyStatus`設定的隱私權狀態。 將狀態設定為`PRIVACY_STATUS_OPT_OUT`會隱藏所有資料集合。

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

若要還原追蹤，請將狀態設回opted in：

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

您也可以在您的`ADBMobileConfig.json`檔案中，於SDK初始化時設定預設隱私權狀態：

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB 媒體收集API]

Media Collection API是伺服器端實作。 您的應用程式必須先檢查使用者同意狀態，才能進行API呼叫並抑制選擇退出使用者的請求。

對於完整選擇退出，對於選擇退出的使用者，請勿對工作階段端點進行POST。

針對CCPA下的部分選擇退出，請在`sessionStart`請求的`params`物件中包含選擇退出旗標：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`：設為`true`，可選擇退出在Adobe Analytics與其他Experience Cloud解決方案（例如Audience Manager）之間共用的資料。
* `analytics.optOutShare`：設定為`true`可選擇退出與其他Adobe Analytics使用者端的同盟資料共用。

如需可用引數的完整清單，請參閱[媒體收集API要求引數參考](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)。

>[!ENDTABS]

