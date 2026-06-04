---
title: 設定適用於串流媒體的Web SDK標籤擴充功能
description: 在Adobe Experience Platform Web SDK標籤擴充功能中設定串流媒體收集。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 設定適用於串流媒體的Web SDK標籤擴充功能

Adobe Experience Platform Web SDK標籤擴充功能可讓您在資料收集UI中設定串流媒體收集，而不使用`alloy.js`設定代碼。 本頁涵蓋標籤設定。 若要改為在程式碼中設定Web SDK，請參閱[為串流媒體設定Web SDK](web-sdk.md)。

* **必要條件**：
   * 完成[Edge實作總覽](overview.md) （結構描述、資料集、啟用[!UICONTROL Media Analytics]的資料流）。
   * 安裝及設定網頁SDK標籤擴充功能。 請參閱[Web SDK標籤擴充功能概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/extensions/client/web-sdk/overview)。

## 在擴充功能中設定串流媒體

1. 在資料收集UI中，開啟您的Web屬性並選取&#x200B;**[!UICONTROL 擴充功能]**。
1. 在已安裝的&#x200B;**Adobe Experience Platform Web SDK**&#x200B;擴充功能上，選取&#x200B;**[!UICONTROL 設定]**。
1. 展開&#x200B;**[!UICONTROL 串流媒體]**&#x200B;區段並設定下列專案：
   * **[!UICONTROL 頻道]** — 每個工作階段報告的頻道名稱。
   * **[!UICONTROL 播放器名稱]** — 使用中的媒體播放器名稱。
   * **[!UICONTROL 應用程式版本]** — 您的播放器應用程式的版本。
   * **[!UICONTROL 主要Ping間隔]**&#x200B;和&#x200B;**[!UICONTROL 廣告Ping間隔]** — 主要內容和廣告的Ping步調（以秒為單位）。
1. 儲存擴充功能組態並發佈變更。

## 追蹤媒體事件

設定擴充功能後，請使用&#x200B;**[!UICONTROL 傳送事件]**&#x200B;動作（或`sendEvent`命令）傳送每個媒體事件。 檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**網頁SDK**&#x200B;標籤，以取得確切的裝載。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [網頁SDK標籤延伸總覽](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [設定串流媒體Web SDK （程式碼）](web-sdk.md)
>* [事件總覽](/help/implementation/events/overview.md)
