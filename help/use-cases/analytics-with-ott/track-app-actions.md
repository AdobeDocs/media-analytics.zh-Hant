---
title: 追蹤應用程式動作
description: 應用程式動作為發生在您要測量之應用程式中的事件。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 100%

---

# 追蹤應用程式動作{#track-app-actions}

動作為發生在您要測量之應用程式中的事件。

每個動作有一或多個對應量度，會隨著每次事件發生而增量。 例如，您可能會針對每個新訂閱、每次對內容進行分級或每次完成某個層級時，傳送 `trackAction` 呼叫。

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
