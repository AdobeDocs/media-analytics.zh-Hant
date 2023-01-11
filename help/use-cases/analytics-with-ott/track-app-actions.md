---
title: 追蹤應用程式動作
description: 應用程式動作為發生在您要測量之應用程式中的事件。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '132'
ht-degree: 100%

---

# 追蹤應用程式動作{#track-app-actions}

動作為發生在您要測量之應用程式中的事件。

每個動作有一或多個對應量度，會隨著每次事件發生而增量。例如，您可能會針對每個新訂閱、每次對內容進行分級或每次完成某個層級時，傳送 `trackAction` 呼叫。

應用程式不會自動追蹤動作，因此您必須在要追蹤的事件發生時呼叫 `trackAction`，然後將動作對應至自訂事件。

1. 在要追蹤的事件發生時呼叫 `trackAction`。

   * **Roku：**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast：**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. 將動作對應至自訂事件。

   * **Roku：**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast：**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

您還可以隨著每次追蹤動作呼叫傳送其他內容資料。
