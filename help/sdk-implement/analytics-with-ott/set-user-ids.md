---
seo-title: 設定使用者 ID
title: 設定使用者 ID
uuid: fdd54fec-79cd-4fb8-b17 e-4d61 d84 f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

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
