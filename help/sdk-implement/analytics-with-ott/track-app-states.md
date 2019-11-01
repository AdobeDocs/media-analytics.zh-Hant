---
title: 追蹤應用程式狀態
description: '應用程式狀態是您應用程式中不同的畫面或檢視，當顯示時應會產生trackState呼叫。 '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 追蹤應用程式狀態{#track-app-states}

狀態是您的應用程式中不同的畫面或檢視。每次在應用程式中顯示新狀態時，您都應傳送呼 `trackState` 叫。 例如，當使用者從首頁導覽至視訊詳細資料畫面時，請傳送呼 `trackState` 叫。 狀態通常是透過路徑報表來檢視，所以您可以瞭解使用者如何導覽應用程式以及最常檢視哪些狀態。

## trackState呼叫

您通常會在應 `trackState` 用程式每次載入新畫面時呼叫。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 在其他Analytics介面中，「檢視狀態」報告為「頁面名稱」;「狀態檢視」會報告為「頁面檢視」。

## 傳送上下文資料

除了「狀態名稱」外，您還可以透過每個追蹤狀態呼叫傳送其他上下文資料。

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
>內容資料值必須對應至 Adobe Mobile Services 中的自訂變數.

