---
title: 設定適用於串流媒體的Roku Edge
description: 設定Adobe Experience Platform Roku SDK將串流媒體資料傳送至Edge Network。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# 設定適用於串流媒體的Roku Edge

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript)會收集Roku頻道中的媒體工作階段資料，並將其傳送至Edge Network。 Roku是在程式碼中設定，不使用標籤。

* **必要條件**：
  * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
  * 從[GitHub版本](https://github.com/adobe/aepsdk-roku/releases)下載SDK並將其新增至您的頻道，如[快速入門手冊](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md)中所述。

## 設定適用於媒體的Roku Edge SDK

初始化SDK並設定資料流和媒體設定：

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

然後開啟具有`createMediaSession`的工作階段：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>在播放期間使用最新的播放點值，每秒至少傳送一次`media.ping`事件。 Roku Edge SDK需仰賴這些Ping才能正常運作。

如需設定金鑰和完整API的資訊，請參閱[Roku Edge SDK API參考](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md)。

## 追蹤媒體事件

在工作階段開啟後，傳送每個媒體事件並附上`sendMediaEvent`。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Roku Edge**&#x200B;索引標籤，以取得確切的負載。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
