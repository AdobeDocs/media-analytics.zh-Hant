---
title: 什麼是媒體串流歸因？
description: 了解如何將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 87%

---

# 媒體串流歸因 {#media-stream-attribution}

使用媒體串流歸因，您可以將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。

## 媒體追蹤以外的媒體維度

您可以將媒體維度新增到分析呼叫中，例如頁面檢視和自訂連結。在實作期間，您必須將媒體內容資料參數新增到 Analytics 追蹤呼叫。若要檢視用於媒體的可用內容資料參數的完整清單，請參閱[音訊和視訊參數](/help/implementation/variables/audio-video-parameters.md)。

若要為特定報告啟用此功能，請從 Admin console 重新啟用媒體追蹤設定。

>[!NOTE]
>
>媒體量度&#x200B;_不_&#x200B;可用於媒體追蹤以外，因為其中大多數是由串流媒體收集附加元件根據心率事件計算。 此外，請務必確保媒體量度不會因不同的實作而膨脹。

## 使用媒體串流歸因

下列 JavaScript 範例將產生「自訂連結」追蹤呼叫，且名稱會設為「Hero Banner」。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 報表中，您可以使用 `Show` eVar 來劃分資料，且將能計算追蹤連結例項的數目。報表看起來類似以下畫面：

![](/assets/myShow-rpt-1.png)

## 使用個案

下列範例顯示了以下內容的使用案例：

* 類別位置
* Hero 位置
* 參與
* 訂閱

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
