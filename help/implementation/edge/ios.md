---
title: 設定適用於串流媒體的iOS
description: 在iOS上設定Adobe Experience Platform Mobile SDK，將串流媒體資料傳送至Edge Network。
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
source-wordcount: '239'
ht-degree: 0%
---
# 設定適用於串流媒體的iOS

Adobe Streaming Media for Edge Network擴充功能(`AEPEdgeMedia`)會收集iOS或tvOS應用程式中的媒體工作階段資料，並將其傳送至Edge Network。 本頁說明程式碼內設定。 若要改為透過Tags行動屬性設定SDK，請參閱[為含有標籤的串流媒體設定iOS](ios-tags.md)。

* **必要條件**：
  * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
  * 將`AEPCore`、`AEPEdge`、`AEPEdgeIdentity`和`AEPEdgeMedia`擴充功能新增至您的應用程式。 如需安裝和註冊，請參閱[Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)。

## 設定iOS的媒體

在初始化SDK時設定媒體設定索引鍵：

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

接著建立追蹤器以管理媒體工作階段：

```swift
let tracker = Media.createTracker()
```

如需組態金鑰和完整的追蹤器API，請參閱[Edge Network API參考媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)。

## 追蹤媒體事件

建立追蹤器後，請使用其追蹤器方法來追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**iOS**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [適用於Edge Network的Adobe串流媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [設定具有標籤的串流媒體的iOS](ios-tags.md)
>* [事件總覽](/help/implementation/events/overview.md)
