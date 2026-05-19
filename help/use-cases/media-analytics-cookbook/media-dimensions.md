---
title: 什麼是媒體串流歸因？
description: 了解如何將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e4f5f438-eabb-4c54-9133-b817e3d125f5
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# 媒體串流歸因 {#media-stream-attribution}

使用媒體串流歸因，您可以將應用程式動作連結到媒體追蹤資料，而不需要其他處理規則和自訂變數。

## 媒體追蹤以外的媒體維度

您可以將媒體維度新增到分析呼叫中，例如頁面檢視和自訂連結。 在實作期間，您必須將媒體內容資料參數新增到 Analytics 追蹤呼叫。

若要為特定報告啟用此功能，請從 Admin console 重新啟用媒體追蹤設定。

>[!NOTE]
>
>媒體量度&#x200B;_不_&#x200B;可用於媒體追蹤以外，因為其中大多數是由串流媒體服務根據心率事件計算。 此外，請務必確保媒體量度不會因不同的實作而膨脹。

## 使用媒體串流歸因

下列 JavaScript 範例將產生「自訂連結」追蹤呼叫，且名稱會設為「Hero Banner」。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 報表中，您可以使用 `Show` eVar 來劃分資料，且將能計算追蹤連結例項的數目。 報表看起來類似以下畫面：

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
