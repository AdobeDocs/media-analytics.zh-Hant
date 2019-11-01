---
title: 設定使用者 ID
description: 用於設定使用者ID的API，該伺服器是唯一的客戶識別碼。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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
