---
seo-title: 追蹤應用程式動作
title: 追蹤應用程式動作
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# 追蹤應用程式動作{#track-app-actions}

動作為發生在您要測量之應用程式中的事件。

每個動作有一或多個對應度量，會隨著每次事件發生而增量。For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

應用程式不會自動追蹤動作，因此您必須在要追蹤的事件發生時呼叫 `trackAction`，然後將動作對應至自訂事件。

1. When an event that you want to track occurs, call `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. 將動作對應至自訂事件。

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

您還可以隨著每次追蹤動作呼叫傳送其他內容資料。

