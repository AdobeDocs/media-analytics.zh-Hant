---
title: 追蹤應用程式狀態
description: 應用程式狀態是您的應用程式中不同的畫面或檢視。 了解如何使用 trackState 呼叫追蹤應用程式中的應用程式狀態。
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 100%

---

# 追蹤應用程式狀態{#track-app-states}

狀態是您的應用程式中不同的畫面或檢視。 每次在您的應用程式中顯示新狀態時，您應傳送 `trackState` 呼叫。 例如，當使用者從首頁導覽至視訊詳細資料畫面時，請傳送 `trackState` 呼叫。 狀態通常是透過路徑報表來檢視，所以您可以瞭解使用者如何導覽應用程式以及最常檢視哪些狀態。

## trackState 呼叫

每次在應用程式載入新畫面時，您通常會呼叫 `trackState`。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

在 Adobe Mobile Services 中，State Name 是在「View State」變數中回報，且每次 `trackState` 呼叫的檢視都會記錄下來。 在其他 Analytics 介面中，「檢視狀態」會回報為「頁面名稱」；「狀態檢視」會回報為「頁面檢視」。

## 傳送內容資料

除了「State Name」之外，您還可以隨著每次追蹤狀態呼叫傳送其他內容資料。

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>內容資料值必須對應至 Adobe Mobile Services 中的自訂變數。
