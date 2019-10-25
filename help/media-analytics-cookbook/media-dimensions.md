---
title: 媒體串流歸因
seo-title: 媒體串流歸因
translation-type: tm+mt
source-git-commit: cc067b31066aa5d7e254167e32429c6c56e40c77

---


# 媒體串流歸因

此功能可讓您將應用程式動作連結至媒體追蹤資料，而不需要額外的處理規則和自訂變數。

## 媒體追蹤以外的媒體維度

透過「媒體串流歸因」，客戶現在可以將任何媒體維度新增至所有其他分析呼叫，例如頁面檢視和自訂連結。 在實作期間，您必須將媒體內容資料參數新增至Analytics追蹤呼叫。 媒體上使用的上下文資料參數完整清單可從以下網址取得：音 [訊和視訊參數。](/help/metrics-and-metadata/audio-video-parameters.md)

您也需要從管理控制台重新啟用媒體追蹤設定，以便針對每個要啟用此功能的報表進行媒體追蹤設定。

>[!NOTE]
>媒體量度不 _能用於_ 「媒體追蹤」以外的位置，因為大部分量度是由媒體分析計算
>基於心率事件。 此外，媒體量度不要因不同實作而誇大也很重要。

## 做法

以下JavaScript範例將產生名稱設為「英雄橫幅」的自訂連結追蹤呼叫。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在Analytics報表中，您可以使 `Show` 用eVar來劃分資料，並且可以計算追蹤連結例項。 報表看起來類似：

![](/assets/myShow-rpt-1.png)

## 使用個案

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

