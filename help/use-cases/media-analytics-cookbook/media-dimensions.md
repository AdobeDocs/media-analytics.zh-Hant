---
title: 什麼是媒體資料流歸因？
description: 了解如何將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 39%

---

# 媒體串流歸因 {#media-stream-attribution}

透過媒體資料流歸因，您可以將應用程式動作連結至媒體追蹤資料，而不需要其他處理規則和自訂變數。

## 媒體追蹤以外的媒體維度

您可以將媒體維度新增至分析呼叫，例如頁面檢視和自訂連結。 在實施期間，您必須將媒體內容資料參數新增到 Analytics 追蹤呼叫。若要檢視媒體專用可用內容資料參數的完整清單，請參閱 [音訊和視訊參數。](/help/implementation/variables/audio-video-parameters.md)

若要為特定報表啟用此功能，請從管理控制台重新啟用媒體追蹤設定。

>[!NOTE]
>
>媒體量度包括 _not_ 可在媒體追蹤之外使用，因為其中大多數是由串流媒體分析根據心率事件計算。 此外，請務必確保媒體量度不會因不同的實施而膨脹。

## 使用媒體資料流歸因

以下的JavaScript範例會產生自訂連結追蹤呼叫，其名稱會設為「Hero Banner」。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 報表中，您可以使用 `Show` eVar 來劃分資料，且將能計算追蹤連結例項的數目。報表看起來類似以下畫面:

![](/assets/myShow-rpt-1.png)

## 使用個案

下列範例顯示下列的使用案例：

* 類別位置
* 主圖版位
* 參與
* 訂閱

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
