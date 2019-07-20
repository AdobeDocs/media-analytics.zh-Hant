---
seo-title: 追蹤應用程式狀態
title: 追蹤應用程式狀態
uuid: 2f98fb43-c362-4a9 b-8732-fa7 e963 da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# 追蹤應用程式狀態{#track-app-states}

狀態是您的應用程式中不同的畫面或檢視。Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. 狀態通常是透過路徑報表來檢視，所以您可以瞭解使用者如何導覽應用程式以及最常檢視哪些狀態。

## trackState呼叫

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 在其他Analytics介面中，「檢視狀態」報告為「頁面名稱」；「狀態檢視」報告為「頁面檢視」。

## 傳送上下文資料

除了「州名稱」外，您也可以隨每個追蹤狀態呼叫傳送其他上下文資料。

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

