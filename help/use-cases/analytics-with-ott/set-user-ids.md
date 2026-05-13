---
title: 設定使用者 ID
description: 設定使用者 ID 的 API，做為唯一客戶識別碼。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: Streaming Media, API
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/AG7KGMEVhpDbGzHKhb94KF8QHzDTw-y1kdkklOdWCFI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 53
ht-degree: 69%

---

# 設定使用者 ID{#set-user-ids}

使用者ID是應用程式為使用者定義的唯一自訂訪客識別碼。

依照下列步驟，在 ADBMobile SDK 上設定並取得唯一使用者 ID：

* **設定：**

   * **Roku：**

     ```
     ADBMobile().setUserIdentifer("app-generated-unique-id")
     ```

   * **Chromecast：**

     ```
     ADBMobile().config.setUserIdentifer("app-generated-unique-id");
     ```

* **取得：**

   * **Roku：**

     ```
     vid = ADBMobile().userIdentifer()
     ```

   * **Chromecast：**

     ```
     vid = ADBMobile().config.getUserIdentifer();
     ```
