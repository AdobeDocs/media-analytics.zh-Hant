---
title: 設定適用於串流媒體的iOS及其標籤
description: 使用iOS適用的Adobe串流媒體標籤擴充功能設定Edge Network的串流媒體收集。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 設定適用於串流媒體的iOS及其標籤

您可以透過「標籤」行動屬性來設定iOS或tvOS應用程式的串流媒體收集，並在資料收集UI中管理媒體設定。 本頁涵蓋標籤設定。 若要改為在程式碼中設定SDK，請參閱[為串流媒體設定iOS](ios.md)。

* **必要條件**：
   * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
   * 在資料收集UI中建立行動屬性。 請參閱[適用於Edge Network的Adobe串流媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)。

## 設定擴充功能

1. 在資料彙集UI中，開啟您的行動屬性並選取&#x200B;**[!UICONTROL 擴充功能]**。
1. 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤上，找到&#x200B;**Adobe Streaming Media for Edge Network**&#x200B;擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。
1. 設定下列專案，然後儲存：
   * **[!UICONTROL 頻道]** — 每個工作階段報告的頻道名稱。
   * **[!UICONTROL 播放器名稱]** — 使用中的媒體播放器名稱。
   * **[!UICONTROL 應用程式版本]** — 您的播放器應用程式的版本。
1. 發佈您的變更，然後將`AEPCore`、`AEPEdge`、`AEPEdgeIdentity`和`AEPEdgeMedia`相依性新增至您的應用程式，並註冊至行動核心。

## 追蹤媒體事件

發佈屬性並建立追蹤器後，可使用其追蹤器方法追蹤每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**iOS**&#x200B;索引標籤，以取得確切的呼叫。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [適用於Edge Network的Adobe串流媒體](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [設定適用於串流媒體的iOS （程式碼）](ios.md)
>* [事件總覽](/help/implementation/events/overview.md)
