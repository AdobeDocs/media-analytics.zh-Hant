---
title: 設定使用者 ID
description: 設定使用者 ID 的 API，做為唯一客戶識別碼。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: '"Media Analytics, API"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 94%

---

# 設定使用者 ID{#set-user-ids}

使用者 ID 是應用程式為設定者定義的唯一自訂訪客識別碼。

依照下列步驟，在 ADBMobile SDK 上設定並取得唯一使用者 ID:

* **設定:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **取得:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
