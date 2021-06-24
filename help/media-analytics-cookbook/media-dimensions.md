---
title: 什麼是媒體資料流歸因？
description: 了解如何將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 97%

---

# 媒體資料流歸因

此功能可讓您將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。

## 媒體追蹤以外的媒體維度

透過媒體資料流歸因，客戶現在可以將任何媒體維度新增到所有其他分析呼叫，例如頁面檢視和自訂連結。在實施期間，您必須將媒體內容資料參數新增到 Analytics 追蹤呼叫。您可以在這裡取得媒體專用內容資料參數的完整清單: [音訊和視訊參數](/help/metrics-and-metadata/audio-video-parameters.md)。

針對您要啟用此功能的每個報表，您也必須從 Admin Console 重新啟用媒體追蹤設定。

>[!NOTE]
>
>媒體量度&#x200B;_無法_&#x200B;用於媒體追蹤以外，因為其中大多數是由 Media Analytics 根據心率事件計算。此外，請務必確保媒體量度不會因不同的實施而膨脹。

## 做法

下列 JavaScript 範例將產生「自訂連結」追蹤呼叫，且名稱會設為「Hero Banner」。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 報表中，您可以使用 `Show` eVar 來劃分資料，且將能計算追蹤連結例項的數目。報表看起來類似以下畫面:

![](/assets/myShow-rpt-1.png)

## 使用個案

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
