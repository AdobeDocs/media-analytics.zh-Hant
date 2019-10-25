---
seo-title: 在播放期間處理應用程式中斷
title: 在播放期間處理應用程式中斷
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 在播放期間處理應用程式中斷{#handling-application-interrupts-during-playback}

媒體應用程式中的播放可透過多種方式中斷：使用者會明確按下暫停，或當使用者將應用程式置入背景時。 不論媒體播放中斷的原因為何，追蹤指示都相同：

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. 如此會導致播放至該時段不會計入總播放時間，並遺失先前的進度標籤、區段等。 Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## 有關如何處理應用程式中斷的常見問題集: {#faq-about-handling-application-interrupts}

* _應用程式要在背景停留多長的時間後，才應關閉工作階段?_

   如果應用程式允許背景播放，它能呼叫我們的 API 來繼續追蹤，我們也會照常傳送所有追蹤 Ping。除了YouTube Red之外，許可背景播放的視訊應用程式不多，但是所有音訊應用程式都允許。 如果應用程式不允許背景播放，則建議您在暫停狀態停留一分鐘，然後結束追蹤工作階段。 應用程式無法繼續傳送「暫停」ping，因為在大多數情況下，它無法判斷使用者是要返回繼續檢視媒體，還是決定何時會停止檢視媒體。 如果應用程式停留在背景時繼續傳送 Ping，也會帶來不良的體驗。

* _應用程式長時間停留在背景之後，要怎麼處理重新啟動追蹤才是正確的做法?_

   應用程式應呼叫 `trackSessionEnd` 來結束追蹤工作階段。從 2.1 版開始，SDK 會傳送「結束」Ping 來通知後端追蹤工作階段已關閉。

* _要如何重新啟動同一個工作階段?_

   如需重新啟動追蹤工作階段的詳細指示，請參閱頁面: [
繼續非作用中工作階段。](/help/sdk-implement/cookbook/resuming-inactive.md)SDK 會傳送恢復 Ping 來通知後端，告知它使用者正在手動恢復工作階段。

