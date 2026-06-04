---
title: 設定適用於串流媒體的Android
description: 在Android上設定Adobe Experience Platform Mobile SDK，將串流媒體資料傳送至Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 設定適用於串流媒體的Android

Adobe Streaming Media for Edge Network擴充功能(`EdgeMedia`)會在Android應用程式中收集媒體工作階段資料，並將其傳送至Edge Network。 本頁說明程式碼內設定。 若要改為透過Tags行動屬性設定SDK，請參閱[為含有標籤的串流媒體設定Android](android-tags.md)。

* **必要條件**：
   * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
   * 將`Core`、`Edge`、`EdgeIdentity`和`EdgeMedia`擴充功能新增至您的應用程式。 如需安裝和註冊，請參閱[Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)。

## 設定Android的媒體

在初始化SDK時設定媒體設定索引鍵：

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

接著建立追蹤器以管理媒體工作階段：

```kotlin
val tracker = Media.createTracker()
```

如需組態金鑰和完整的追蹤器API，請參閱[Edge Network API參考媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)。

## 追蹤媒體事件

建立追蹤器後，請使用其追蹤器方法來追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Android**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [適用於Edge Network的Adobe串流媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [設定具有標籤的串流媒體的Android](android-tags.md)
>* [事件總覽](/help/implementation/events/overview.md)
